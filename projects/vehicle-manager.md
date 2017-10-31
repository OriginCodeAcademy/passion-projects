# Vehicle Manager (Backend)

## 1. Build the Backend

### 1a. Setup the Project

First, create a folder to store the back-end for this project:

```bash
$ mkdir -p ~/oca/passion-projects/vehicle-manager/backend
```

Next, navigate to that folder and initialize a new `npm` project

```bash
$ cd ~/oca/passion-projects/vehicle-manager/backend
$ git init
$ npm init
```

This will prompt you to answer some questions, such as the name of your project; a brief description; author names etc. If you don't know what to enter for a particular field, just hit enter/return to skip the question.

At this point, run through the [Idiomatic Express Drill](https://gist.github.com/cameronwilby/76489153e00aaf3423abfaa2dc2d1884#method-3---idiomatic-folder-structure) to get to a good starting point for the backend.

### 1b. Setup your Model Layer

Once you have created your base Express app, you can focus on creating your models.

![](http://i.imgur.com/Oy1FmSv.png)

Choose either [Sequelize](http://docs.sequelizejs.com/) or [Mongoose](http://mongoosejs.com/) to create these tables in [MySQL](https://www.mysql.com/) or [MongoDB](https://www.mongodb.com/) respectively.

#### `Vehicle` Entity

| Name        | Type  | Note                                            |
| ----------- | ------| ------------------------------------------------|
| vehicleId   | int   | Primary Key / ObjectId                          |
| make        | string| The make of the vehicle (e.g. Ford, Toyota)     |
| model       | string| The model of the vehicle (e.g. Mustang, Corolla)|
| year        | int   | The year the vehicle was released               |
| color       | string| The color of the vehicle                        |
| vehicleType | string| The type of vehicle (e.g. Sedan, Hatchback)     |
| retailPrice | ?     | The price of the vehicle                        |

#### `Customer` Entity

| Name         | Type   | Note                                                |
| ------------ | ------ | ----------------------------------------------------|
| customerId   | int    | Primary Key / ObjectId                              |
| firstName    | string | Customer first name                                 |
| lastName     | string | Customer last name                                  |
| emailAddress | string | Customer email address                              |
| telephone    | ?      | Customer telephone                                  |
| dateOfBirth  | ?      | Customer date of birth (should be an optional field)|

#### `Sale` Entity

| Name        | Type | Note                                                |
| ----------- | ---- | --------------------------------------------------- |
| saleId      | int  | Primary Key / ObjectId                              |
| vehicleId   | ?    | Foreign key / reference to the `Vehicle` being sold |
| customerId  | ?    | Foreign key / reference to the `Customer` sold to   |
| salePrice   | ?    | The final sale price of the vehicle                 |
| invoiceDate | ?    | Date invoice was sent                               |
| paymentDate | ?    | Date payment was fully received                     |

#### Bonus Entity

If you want to add more complexity to the project, add a `Payment` table and make up some properties. In terms of the relationships this new table will require, a `Sale` will have many `Payments`, and a `Customer` will have many payments. You don't need to relate `Payment` with `Vehicle` - because `Payment` is already associated with `Sale`, which in turn is already associated with `Vehicle`.

### 1c. Setup Express Routes

Once you have built your models, build out the following express routes:

#### `/api/vehicles`

| Verb     | Route               | Description       |
| -------- | ------------------- | ----------------- |
| `GET`    | `/api/vehicles/`    | Get all vehicles  |
| `GET`    | `/api/vehicles/:id` | Get a single sale |
| `POST`   | `/api/vehicles/`    | Create a vehicle  |
| `PUT`    | `/api/vehicles/:id` | Update a vehicle  |
| `DELETE` | `/api/vehicles/:id` | Delete a vehicle  |

#### `/api/sales`

| Verb     |Route            | Description   |
| -------- |---------------- | ------------- |
| `GET`    |`/api/sales/`    | Get all sales |
| `GET`    |`/api/sales/:id` | Get single    |
| `POST`   |`/api/sales/`    | Create a sale |
| `PUT`    |`/api/sales/:id` | Update a sale |
| `DELETE` |`/api/sales/:id` | Delete a sale |

#### `/api/customers`

| Verb     |Route            | Description   |
| -------- |---------------- | ------------- |
| `GET`    |`/api/sales/`    | Get all sales |
| `GET`    |`/api/sales/:id` | Get single    |
| `POST`   |`/api/sales/`    | Create a sale |
| `PUT`    |`/api/sales/:id` | Update a sale |
| `DELETE` |`/api/sales/:id` | Delete a sale |

> Use [Postman](https://www.getpostman.com/) to test your routes - it allows you to issue the four main HTTP requests (`GET`, `POST`, `PUT`, and `DELETE`) as well as see additional information such as response time and status code.

### 1d. Write Tests

Setup `mocha` and `chai` in your project, then write unit tests for every route in your express application.

### 1e. Backend Exit Criteria

- Models are created and can successfully store information in a database
- Full test coverage for your express routes
- All tests are passing

---

`DO NOT CONTINUE UNTIL YOU HAVE A WORKING BACKEND SOLUTION!`

---

## 2. Build the Frontend

### 2a. Setup the project

First, create a folder to store the back-end for this project, then use [Create React App](https://github.com/facebookincubator/create-react-app) to scaffold your React app.

```bash
$ mkdir -p ~/oca/passion-projects/vehicle-manager/frontend
```

### 2b. Build the following screens:

The image below outlines the screens to be built for this single page application.

![](https://snag.gy/bxRi5V.jpg)

#### Dashboard
---

The dashboard is the first page the user will see upon opening the application. It should show users high-level reports such as monthly customer acquisition, monthly revenue, monthly profits, etc.

> Put a placeholder page here for now, and focus your efforts on the other 6 screens.

#### Vehicles Grid
---

<img src="https://i.imgur.com/i3vFs0b.png" height="360" />

The vehicles grid should present the user with a table containing all vehicles. This screen should use the `/api/vehicles` route in your Express app.

The table should contain the following columns:

- Full Name
- Email Address
- Telephone
- Outstanding Sales
- Paid Sales (# of sales where payment date is not null)
- Edit Button (Link to detail page with url e.g. `/customers/detail/1`)
- Remove Button (Remember to confirm with user!)


#### Vehicle Detail
---

<img src="https://i.imgur.com/iDCjrZF.png" height="360" />

The vehicle detail screen doubles as both a Create and Edit screen, based on the presence of an `id` parameter in the URL.

This screen should contain the following elements

- First name input
- Last name input
- Email input
- Telephone input 
- Date of Birth input
- Table of Sales (optional)
  - Reuse the markup from the Sales Grid page.

#### Customers Grid
---

<img src="https://i.imgur.com/dbDcTof.png" height="360" />

The customers grid should present the user with a table containing all customers. This screen should use the `/api/customers` route in your Express app.

The table should contain the following columns:

- Full Name
- Email Address
- Telephone
- Outstanding Sales
- Paid Sales (# of sales where payment date is not null)
- Edit Button (Link to detail page with url e.g. `/customers/detail/1`)
- Remove Button (Remember to confirm with user!)
	
> Note: **Outstanding Sales** and **Paid Sales** should be calculated in the back-end. If you are using `mongoose`, you should use [instance methods](http://mongoosejs.com/docs/guide.html#methods) to have these fields be automatically calculated for all customers as they are read from the database.

#### Customer Detail
---

<img src="https://i.imgur.com/RXgQVsn.png" height="360" />

The customer detail screen doubles as both a Create and Edit screen, based on the presence of an `id` parameter in the URL.

This screen should contain the following elements

- First name input
- Last name input
- Email input
- Telephone input 
- Date of Birth input
- Table of Sales (optional)
  - Reuse the markup from the Sales Grid page.

> Note: To include sales for a customer when fetching a customers data from `/api/customers/:id`, your backend should use a technique like [population]() in Mongoose, or [eager loading]() in Sequelize in order to include the related sales for a customer as a nested collection within the customer object.

#### Sales Grid
---

<img src="https://i.imgur.com/mb7ffgu.png" height="360" />

The sales grid presents the user with a table containing all sales. This screen should make use of the `/api/sales` route you made earlier.

The table should contain the following columns:

- Customer Name
- Vehicle Year, Make, Model
- Invoiced? (Should be either "Yes" or "No", depending on whether invoicedDate is null)
- Paid? (See above, extrapolate for paymentReceived.)
- Sale Price
- Edit Button (Link to detail page with url e.g. `/sales/detail/1`)
- Remove Button (Remember to confirm with user!)

#### Sale Detail
---

<img src="https://i.imgur.com/uSyjy5O.png" height="360" />

The sale detail screen doubles as both a Create and Edit screen, based on the presence of an `id` parameter in the URL.

This screen should contain the following inputs:

- Customer dropdown (Use [`react-select`](http://jedwatson.github.io/react-select/) for additional complexity)
- Vehicle dropdown
- Sale Price
- Invoice Date
- Payment Received Date
