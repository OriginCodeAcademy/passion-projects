# Coffee House (Backend)

## 1. Build the Backend

### 1a. Setup the Project

First, create a folder to store the back-end for this project:

```bash
$ mkdir -p ~/oca/passion-projects/coffee-house/backend
```

Next, navigate to that folder and initialize a new `npm` project

```bash
$ cd ~/oca/passion-projects/coffee-house/backend
$ git init
$ npm init
```

This will prompt you to answer some questions, such as the name of your project; a brief description; author names etc. If you don't know what to enter for a particular field, just hit enter/return to skip the question.

At this point, run through the [Idiomatic Express Drill](https://gist.github.com/cameronwilby/76489153e00aaf3423abfaa2dc2d1884#method-3---idiomatic-folder-structure) to get to a good starting point for the backend.

### 1b. Setup your Model Layer

Once you have created your base Express app, you should focus on defining the following models using either [Sequelize]() or [Mongoose](), then define the relationships between them (e.g. one `Customer` record may have many related `Sales`  records.)

You can use either [Sequelize](http://docs.sequelizejs.com/) or [Mongoose](http://mongoosejs.com/) to store your data in [MySQL](https://www.mysql.com/) or [MongoDB](https://www.mongodb.com/) respectively.

#### `Product` Entity

| Name       | Type   | Note                                           |
| -----------| -------| -----------------------------------------------|
| productId  | int    | Primary Key / ObjectId                         |
| name       | string | The name of the drink (e.g. Coffee, Latte)     |
| size       | string | The size of the drink (Small, Medium, or Large)|
| description| string | A quick description of the drink for marketing |
| price      | decimal| The retail price of the product                |

#### `Customer` Entity

| Name         | Type   | Note                                                |
| ------------ | ------ | ----------------------------------------------------|
| customerId   | int    | Primary Key / ObjectId                              |
| firstName    | string | Customer first name                                 |
| lastName     | string | Customer last name                                  |
| emailAddress | string | Customer email address                              |
| telephone    | ?      | Customer telephone                                  |

#### `Sale` Entity

| Name        | Type | Note                                       |
| ----------- | ---- | -------------------------------------------|
| saleId      | int  | Primary key / ObjectId                     |
| customerId  | ?    | Foreign key to the `Customer` for this sale|
| salePrice   | ?    | The final sale price                       |
| invoiceDate | ?    | Date invoice was sent                      |
| paymentDate | ?    | Date payment was fully received            |

### 1c. Setup Express Routes

Once you have built your models, build out the following express routes:

#### `/api/products`

| Verb     | Route               | Description       |
| -------- | ------------------- | ----------------- |
| `GET`    | `/api/products/`    | Get all products  |
| `GET`    | `/api/products/:id` | Get a single sale |
| `POST`   | `/api/products/`    | Create a product  |
| `PUT`    | `/api/products/:id` | Update a product  |
| `DELETE` | `/api/products/:id` | Delete a product  |

#### `/api/sales`

| Verb     |Route            | Description   |
| -------- |---------------- | ------------- |
| `GET`    |`/api/sales/`    | Get all sales |
| `GET`    |`/api/sales/:id` | Get a single sale    |
| `POST`   |`/api/sales/`    | Create a sale |
| `PUT`    |`/api/sales/:id` | Update a sale |
| `DELETE` |`/api/sales/:id` | Delete a sale |

#### `/api/customers`

| Verb     |Route            | Description   |
| -------- |---------------- | ------------- |
| `GET`    |`/api/customers/`    | Get all customers |
| `GET`    |`/api/customers/:id` | Get a single customer    |
| `POST`   |`/api/customers/`    | Create a customer |
| `PUT`    |`/api/customers/:id` | Update a customer |
| `DELETE` |`/api/customers/:id` | Delete a customer |

> Use [Postman](https://www.getpostman.com/) to test your routes - it allows you to issue the four main HTTP requests (`GET`, `POST`, `PUT`, and `DELETE`) as well as see additional information such as response time and status code.

### 1d. Write Tests

Setup `mocha` and `chai` in your project, then write unit tests for all of your express routes.

### 1e. Backend Exit Criteria

- Full test coverage for your express routes
- All tests are passing

---

`DO NOT CONTINUE UNTIL YOU HAVE A WORKING BACKEND SOLUTION WITH UNIT TESTS!`

---

## 2. Build the Frontend

### 2a. Setup the project

First, create a folder to store the back-end for this project, then use [Create React App](https://github.com/facebookincubator/create-react-app) to scaffold your React app.

```bash
$ mkdir -p ~/oca/passion-projects/coffee-house/frontend
```

### 2b. Design and build required screens

#### Product List Screen
---

This screen should:

* Present the user with a list of all products sold by the merchant, using the `GET` express route at `/api/products` as your data source.
* Give users the option to click on a product to view more information.
  * (This must be a link to the `Product Detail Screen`)
* Allow users to click a delete button for a product to remove it from the app.
* Show a confirm dialog to the user before deleting a product using either the native `confirm()` function or [SweetAlert](https://sweetalert.js.org/).

Choose fields you think will make sense for the user to see on this page.

The simplest way to display products is to use a table, you could also research alternatives to tables for displaying collections such as a masonry grid.

#### Product Detail Screen
---

This screen should:

* Present the user with detailed information about a single product, using the `GET` express route at `/api/products/:id` as your data source.
* Allow users to create a product if no `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
* Allow users to update a product if an `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
* Display all sales for the product
  * (You could potentially reuse the React components from the `Sales List Screen` here)

#### Customer List Screen
---

This screen should:

* Present the user with a list of all customers, using the `GET` express route at `/api/customers` as your data source.
* Give users the option to click on a customer to view more information.
  * (This must be a link to the `Customer Detail Screen`)
* Allow users to click a delete button for a customer to remove it from the app.
* Show a confirm dialog to the user before deleting a customer using either the native `confirm()` function or [SweetAlert](https://sweetalert.js.org/).

Choose fields you think will make sense for the user to see on this page.

#### Customer Detail Screen
---

This screen should:

* Present the user with detailed information about a single customer, using the `GET` express route at `/api/customers/:id` as your data source.
* Allow users to create a customer if no `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
* Allow users to update a customer if an `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
* Display all sales for the customer
  * (You could potentially reuse the React components from the `Sales List Screen` here)

#### Sales List Screen
---

This screen should:

* Present the user with a list of all sales, using the `GET` express route at `/api/sales` as your data source.
* Allow users to click an edit button for a sale to view more information.
  * (This must be a link to the `Sale Detail Screen`)
* Allow users to click a delete button for a sale to remove it from the app.
* Show a confirm dialog to the user before deleting a sale using either the native `confirm()` function or [SweetAlert](https://sweetalert.js.org/).

Choose fields you think will make sense for the user to see on this page.

#### Sale Detail Screen
---

This screen should:

* Present the user with detailed information about a single customer, using the `GET` express route at `/api/sales/:id` as a data source.
* Allow users to create a sale if no `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
* Allow users to update a sale if an `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
* Display all information about a customer for the sale
* Display a list of products sold to the customer.

#### Optional: Dashboard Screen
---

> Focus your efforts on the other screens first.

The dashboard would be the first page the user would see upon opening the application. It would show users high-level reports such as monthly customer acquisition, monthly revenue, monthly profits, etc.

You could use a library such as [ChartJS](https://www.google.com/search?q=react+chartjs&oq=react+chartjs&aqs=chrome..69i57.1202j0j4&sourceid=chrome&ie=UTF-8) to create the charts.