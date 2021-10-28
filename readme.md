# Object-Relational Mapping (ORM): E-Commerce Back End
# Table of Contents
  * [Description](#description)
  * [Installation](#installation)
  * [Usage](#usage)
  * [License](#license)
  * [Contributions](#contributions)
  * [Tests](#tests) (not available in this project)
  * [Questions](#questions)
  
  ## Description  
  This is a working E-Commerce backend database created using MySQL, Sequelize, Dotenv, and several other tools feature in the "Built with" section of the readme.  

  VIEW THE APP AT WORK HERE: https://watch.screencastify.com/v/bQ4btkdcPqU61moArXfb


  ## Code Snippets
  Here are some code snippets and what they accomplished. The first code snippet is found in the connection.js file. This connects the app to sequelize which allows a user to use the sequelize library to perform MySQL functionality without using the raw MySQL commands within the MySQL shell. DOTENV is also imported to make use of the database name, user, and password credentials found within a .env file (not uploaded). 
  ```
  const Sequelize = require('sequelize');
  require('dotenv').config();



  const sequelize = process.env.JAWSDB_URL
    ? new Sequelize(process.env.JAWSDB_URL)
    : new Sequelize(
      process.env.DB_NAME,
      process.env.DB_USER,
      process.env.DB_PW,
      {
        host: 'localhost',
        dialect: 'mysql',
        port: 3306,
        dialectOptions: {
          decimalNumbers: true,
        },  
    });

  module.exports = sequelize;
  ```

  This second snippet is the index.js file found within the models directory. This file imports the other model files and uses the sequelize library to establish various relationships (like 1-to-1, 1-to-many, and many-to-many) between them.     
  ```
  const Product = require('./Product');
  const Category = require('./Category');
  const Tag = require('./Tag');
  const ProductTag = require('./ProductTag');

  // Products belongsTo Category
  Product.belongsTo(Category, {
    foreignKey: "category_id",
  });
  // Categories have many Products
  Category.hasMany(Product, {
    foreignKey: "category_id",
  });
  // Products belongToMany Tags (through ProductTag)
  Product.belongsToMany(Tag, {
    through: ProductTag,
    foreignKey: "product_id",
  });
  // Tags belongToMany Products (through ProductTag)
  Tag.belongsToMany(Product, {
    through: ProductTag,
    foreignKey: "tag_id",
  });
  module.exports = {
    Product,
    Category,
    Tag,
    ProductTag,
  };
  ```

  The third snippet is found within the product-routes.js file within the routes directory. Shown is the file importing the Product, Category, Tag, and ProductTag models. The main body of code establishes the basic get routes that one can test with a program such as Insomnia. Here a get request to /api/products will return a list of all products or a singular product if an id is added to the end of the get request. Other routes are set up similarly. 
  ```
   const router = require('express').Router();
   const { Product, Category, Tag, ProductTag } = require('../../models');

    // The `/api/products` endpoint

    // get all products
    router.get('/', (req, res) => {
      // find all products
      // be sure to include its associated Category and Tag data
      Product.findAll(
        {
          include: [
            {
              model: Category,
            },
            {
              model: Tag,
            }
          ]
        }).then(productData => res.json(productData));
    });

    // get one product
    router.get('/:id', (req, res) => {
      // find a single product by its `id`
      // be sure to include its associated Category and Tag data
      Product.findOne(
        {
          where: {
            id: req.params.id
          },
          include: [
            {
              model: Category,
            },
            {
              model: Tag,
            }
          ]
        }).then(oneProduct => res.json(oneProduct));
    });
  ```

  ## Installation
  To install:
  ```
  Once you have a working SSH key added to your Github account, go to the ecommerce-backend repository. Click the green "code" button on the top right and clonecopy the @github.com link with the SSH key option to your clipboard. 
  ```

  Next, 
  ```
  Open Gitbash or Terminal and navigate to a directory that you would like to add the cloned repository. Once in your desired directory type in
  "git clone 'right click to paste'" and press enter. This will clone the repository onto your personal machine.
  ```
  Lastly, 
  ```
  Type 'ls' into your Gitbash or Terminal to see a list of items within the directory. If you have done the previous steps correctly then you should see a respository titled "ecommerce-backend". Simply type in "code ." to open it in your code editor of choice. Lastly, check the package.json file to see the dependencies needed to run this. WIthin your terminal run an npm install. This will give you everything you need to run the app. From there, check the attached screencastify link near the top to see what to do next. 

  ```

  ## Usage
  This backend database, if connected to a client-side frontend, will allow user's to search up a variety of different products based on different search criteria like "category" and product "tags". This also allows for the client to add new products, update existing information, or delete from the database. 

  ## Built With
  * [JAVASCRIPT](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
  * [NODE.JS](https://nodejs.org/en/)
  * [EXPRESS.JS](https://expressjs.com/)
  * [MYSQL](https://www.mysql.com/)
  * [SEQUELIZE](https://sequelize.org/)
  * [DOTENV](https://www.npmjs.com/package/dotenv)

  ## Deployed Link
* [See the Live Site!](https://tylerbyeager.github.io/ecommerce-backend/) 

## Authors

* **Tyler Brian Yeager**

- [Link to Repo Site](https://github.com/TylerBYeager/ecommerce-backend)
- [Link to Github](https://github.com/TylerBYeager/tylerbyeager.github.io)
- [Link to LinkedIn](https://www.linkedin.com/in/tyler-yeager-611926213/)

## Contributions

- UC Berkeley Coding Bootcamp & my pair programmers this week
- BCS learning assistants helping me get "unstuck" and gain a better understanding in the process

## License
![License](https://img.shields.io/badge/License-Apache-blue.svg)

## Questions
- wow_d2@hotmail.com