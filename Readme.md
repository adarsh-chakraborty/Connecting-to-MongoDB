## Connecting to MongoDB

Connecting & Working with MongoDB Tutorial. We can Install mongodb locally for development but in this Tutorial we are going to use MongoDB Atlas.

### Setting up Clustor

- Login/Register on MongoDB Atlas.
- Create or Use an existing clustor if you already have one provisioned.
- While creating the database, you need to create Credentials for database user/admin.

### Get your Credentials

- After your clustor is provisioned, You can click on connect button.
- On the screen, Click on the option which says Connect your application.
- Copy the mongodb URI string. With this string you can connect with your mongodb.
- The URI looks like this

  > mongodb+srv://adarsh:<password>@cluster0.mongodb.net/myFirstDatabase?retryWrites=true&w=majority

In my case, `adarsh` is the database admin username and <password> has to be replaced by the password you have set.
`/myFirstDatabase` is the database collection you're connecting to, It can be anything, If it doesn't exists mongodb will automatically create the collection for you.

So now, we have got the clustor created, got the username,password & URI.

\*\*\* MongoDB URI

The MongoDB URI string basically contains all the information required to connect to mongodb.

- username:
- <password>
- @Clustor address
- /collection name

### Whitelist your IP

- In the network Access tab, Make sure to add your ip and your server's ip address there
- It's important else you won't be able to connect even with correct Credentials.
- You can also click on Allow Access From Anywhere button which allows all ips to connect to your database.

### Setting up your Node.js Server

Now we need to install mongodb driver in our project.

```
npm i mongodb
```

### Inserting document into Database

After Installing the mongodb driver, import it in the server. We just need the MongoClient from the package.

```javascript
import {MongoClient} from 'mongodb';

async function handler(req,res){

    const client = await MongoClient.connect("mongodb+srv://username:<password>@cluster0.mongodb.net/myDatabaseName?retryWrites=true&w=majority");
    const db = client.db();

    const collectionName = db.collection('collectionName');

    const result = await collectionName.insertOne({req.data});

    client.close();
    res.status(201).json({message: 'Meetup Inserted'});
}
```
