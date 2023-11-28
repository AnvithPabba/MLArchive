# MLArchive - A Hub for ML Models & Datasets

### <b>The PostgreSQL account where your database on our server resides</b> - nj2513 
<br/>

### <b>The URL of your web application</b> - 34.138.224.77 
<br/>

## <b>About the Website - </b>

* Our project is all about creating a helpful tool for people interested in machine learning to upload, download, review and search through models and datasets. 

* It's like a big library that stores lots of machine learning models and datasets, making it easy for anyone to learn and experiment with machine learning. Users can keep track of the most popular/best rated models and datsets while receiving tailored models and dataset recommendations.

<br/>

### <b> Features of the website </b> - 

We were able to implement everything as part of out Part 1 and Part 2 design plan. We made a slight tweak replacing version history with keeping a training log whenever a user trains a model.

* <b> Search through Datasets </b> - Search through the catalog of uploaded datasets based on the name of the dataset or assosciated tags. For example, the user could search for "classification" datasets or "NER" datasets.

* <b> Search through Models </b> - Search through the catalog of uploaded models based on name of the model or assosciated tags. For example, the user could search for "text generation" models, "image classification" models or "NLI" models.

* <b> Search for relevant Authors in a field</b> - A user can search for authors who have published models in a particular field (we take the user input for this) after a particular year (the user inputs this as well).

* <b> Trending Section </b> - When you land on the webpage you see a trending section, which lists the top datasets/models being used in the ML community. We use the review ratings as a metric to rank datasets. For models, we rank it by the number of downloads.

* <b> Citations Page </b> - Here you can look at all the citations associated with every model and dataset.

* <b> User Login </b> - The home page has different functionality depending on whether the user is a <b>free tier user</b> or a <b>premium tier user</b>. As a premium tier, the user gets more functionalities, such as training models on a remote server. 

* <b> User Functionalities </b> - The functionalities on the website differ if the user is either <b> free tier </b> or <b> premium tier </b>. All functionalities of a <b> free tier </b> user is available to the <b> premium tier </b> but not the vice versa. 

    * <b> View Training Logs </b> - Whenever a user trains a model, these logs are saved which the user can look at later. 

    * <b> Upload Models or Datasets </b> - A user can upload models or datasets to the database. When uploading a model, we also edit the pretrained_on table to keep track of what models are pretrained_on which dataset.

    * <b> Download Models or Datasets </b> -  A user can download models or datasets. A free user can download only a limited set of these while a premium user has an infinite access to downloads.

    * <b> Train Models </b> - A premium user with a non-zero compute power can train models. However, as per the model structure a user can train a (model, dataset) pair only once. A user trains a model on a cluster.

    * <b> Write a review </b> - A user can post a text review about the dataset along with rating the dataset on a scale of 0-5.

    * <b> Recommendation System </b> - One interesting aspect here is that, as the user interacts with the interface, the trending section updates itself to show models/datasets that align well with the models/datasets the user has worked with previously and are also better rated in the commmunity. 

<br/>

## <b>Webpages- </b>

* <b> Postlogin page (Homepage) </b> - The post-login or the homepage is the main page connecting to three other pages - Models, Datasets and Citations. A logged in user also has the option to delete their account or sign out, while a guest user will be re-directed to a sign-in page to create a new account and login if needed. The homepage consists of a search bar called "Search_Models_Dataset" that lets users explore models and datasets by names or associated tags. For instance, if a user looks for "classification," the system executes a database query, finding models and datasets that match this criteria. An interesting aspect for premium users is the ability to train a model, in SQL this is equivalent to inserting entries into the table. Users can also check their training history, listing all the models and datasets they've trained before. Another interesting aspect is the trending page which lists all the top models and datasets being used in the community ranked by the number of downloads and average rating respectively. The database operation involves selecting the top 5 and ordering them by these criteria. Moreoever, this list adds a section of "Relevant to you" as users interact with models, providing an update to the recommendations based on their last use. In terms of database operations, we build this recommendation by doing a search over all the models with the tags of the last interacted model.

* <b> Datasets Webpage </b> - The next interesting webpage would be the Datasets webpage which gives the functionality of Downloading, Uploading, Deleting and Reviewing. Delete translates to removing an entry from a table in the database, upload translates to adding a new entry. Downloading saves the information to another table called "download_dataset". Review allows the user to add a text review and a numeric rating to any particular dataset. This also translates to adding data to the database.
<br/>

## <b>Use of AI tools </b>

We used ChatGPT to reproduce comparable HTML files since several webpages adhered to a common template, with only slight variations in the naming. For instance, upload_dataset_form.html and upload_model_form.html share a similar structure, differing primarily in the text content. The following are the queries we used - 

example of the query used: 

-----
&lt;html> <br/>
    &lt;body><br/>
        &lt;h1>Upload Model&lt;/h1><br/>
        &lt;form method="POST" action="/upload_model"><br/>
            &lt;label for="model_name">Model Name:&lt;/label><br/>
            &lt;input type="text" id="model_name" name="model_name" required>
    
            <label for="num_parameters">Number of Parameters:</label>
            <input type="number" id="num_parameters" name="num_parameters" required>
    
            <label for="num_layers">Number of Layers:</label>
            <input type="number" id="num_layers" name="num_layers" required>
    
            <label for="tag1">Tag 1:</label>
            <input type="text" id="tag1" name="tag1" required>
    
            <label for="tag2">Tag 2:</label>
            <input type="text" id="tag2" name="tag2">
    
            <label for="tag3">Tag 3:</label>
            <input type="text" id="tag3" name="tag3">
    
            <label for="num_downloads">Number of Downloads:</label>
            <input type="number" id="num_downloads" name="num_downloads" required>
    
            <label for="username">Username:</label>
            <input type="text" id="username" name="username" required>
    
            <label for="citation_id">Citation ID:</label>
            <input type="number" id="citation_id" name="citation_id" required>
    
            <button type="submit">Upload Model</button>
        </form>
    </body>
&lt;/html>" create something similar for CREATE TABLE User_Uploads_Dataset_With_Citation(
    Dataset_ID int primary key,
    Dataset_name varchar(50) UNIQUE,
    Num_data_points int,
    Num_features int,
    Description varchar(200),
    tag1 varchar(50) NOT NULL,
    tag2 varchar(50),
    tag3 varchar(50),
    Username varchar(20) NOT NULL REFERENCES Customer,
    Citation_ID int NOT NULL REFERENCES Citations,
    CHECK (Num_data_points > 0),
    CHECK (Num_features > 0)
);

<br/>
