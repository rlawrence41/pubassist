# pubassist
Publishers' Assistant

May 9, 2019 - This repository has been created for new PubAssist development.  It should remain private until we have a working model.

Publishers' Assistant is a family of products developed for the publishing industry.  There are many peculiarities to the publishing industry.  Over the years, Publishers' Assistant has been enhanced to support the majority of issues that publishers face.  

At the heart of the existing product is an accounting system that handles most business management functions including: invoicing, receipts, inventory control, etc.  What makes PubAssist unique, however, is the ability to automatically track liabilities associated with your sales.  For example, publishers will regularly pay royalties to authors based on the sales of their books.  PubAssist will allow the publisher to establish very sophisticated royalty contracts, and will track royalties automatically, as the user simply enters invoices and receipts for those sales.

PubAssist, however, is a legacy, PC-based product.  This respository is intended for new development of web-based applications using the LAMP stack.  These applications are intended to replace the functions that are unique to PubAssist over time.

##New Development Overview
PubAssist is a business management software designed for publishing companies. It helps businesses efficiently manage their day-to-day operations, including tracking orders, returns, purchase orders, expenses, and calculating royalties based on sales. PubAssist is a comprehensive solution that streamlines various business functions and is built to support the unique needs of the publishing industry.

The software package includes various web-based applications developed using the LAMP stack, which replace legacy functions from the previous PC-based version of PubAssist. RAPIDS, a core library, plays a crucial role in this transition by generating single-page applications (SPAs) for each data resource. These SPAs allow users to interact with the system's data, making management tasks more efficient and accessible.

##Key Features
Order Management: Track and manage customer orders, returns, and related data.
Purchase Order Tracking: Streamline the creation, approval, and monitoring of purchase orders.
Expense Management: Keep track of business expenses for reporting and decision-making.
Royalty Calculation: Automatically calculate royalties based on sales and other related parameters.
Customizable Reports: Generate reports to provide insights into business performance, including financial data and operational metrics.
System Requirements
Server: A LAMP stack (Linux, Apache, MySQL, PHP)
PHP Version: 7.4 or higher
Database: MySQL or MariaDB (recommended)
Installation
Clone the repository:

bash
Copy code
git clone https://github.com/<your-username>/PubAssist.git

Set up your LAMP stack environment and configure the web server (Apache) to point to the directory where PubAssist is located.

Import the database schema into your MySQL/MariaDB database.

Configure the database connection by editing the config.php file in the app directory.

Deploy the application on your server by visiting the installation URL.

Structure and Components
1. RAPIDS Library
RAPIDS (Rapid API Data Services) is a PHP library that facilitates the generation of single-page applications (SPAs) for each data resource. These SPAs allow users to interact with the system’s database, and they expose a REST API for integration with other applications.

* Generator: The generator.php file in the generator directory is used to create new SPAs for each resource. For example, to generate an application for the contact resource, you would use the following URL:

```
Copy code
https://dev.pubassist.com/generator/generator.php?resource=contact
```

* Generated Applications: The generated SPAs are placed in the demo directory for use. This ensures that each application is available for interaction with the web service while maintaining a clean copy.

2. Example Classes
Below is a sample class generated for the contact resource:

php
Copy code
```
<?php

// contact.class.php - These classes are specific to the contact resource.

class contactPage extends page {
    public function __construct() {
        parent::__construct("contact", "contactPage", "Manage contacts");

        $context = new context("contact", "id");
        $this->context = $context;

        $pageNav = new pageNav("pageNav", "pageNavId", "Manage contacts", "Allows you to navigate to a page within the resource.");
        $pageNav->context = $context;
        $this->addChild($pageNav);

        $table = new contactTable();
        $table->context = $context;
        $this->addChild($table);

        $form = new contactForm("contactForm", "adminForm", "contact");
        $this->addChild($form);
    }
}

class contactTable extends table {
    public function __construct() {
        parent::__construct("contact", "id", "contacts");
        
        $this->addColumn("id", "Id");
        $this->addColumn("contactId", "Contact Id");
        $this->addColumn("company", "Company");
        $this->addColumn("firstName", "First Name");
        $this->addColumn("lastName", "Last Name");
        $this->addColumn("city", "City");
        $this->addColumn("zipCode", "Zip Code");
        $this->addColumn("phone", "Phone");
        $this->addColumn("email", "Email");
    }
}

class contactForm extends form {
    public function __construct(...$args) {
        parent::__construct(...$args);
        $this->addField("readonly", "id", "Id");
        $this->addField("text", "contactId", "Contact Id");
        $this->addField("text", "company", "Company");
        $this->addField("text", "firstName", "First Name");
        $this->addField("text", "lastName", "Last Name");
        $this->addField("text", "city", "City");
        $this->addField("text", "zipCode", "Zip Code");
        $this->addField("text", "phone", "Phone");
        $this->addField("email", "email", "Email");
    }
}
?>

```

3. Application Structure
The structure of the PubAssist application is designed to be easy to navigate and deploy. Key directories include:

/app: Contains the core PHP files for handling business logic.
/generator: Contains the code used to generate SPAs for each resource.
/demo: Contains generated SPAs that are available for the web service.
/config: Contains configuration files for setting up the application environment.
Usage
Once installed, PubAssist is ready for use out of the box. You can log in to the application via the web interface and begin managing your business operations. The system does not require any customization or tailoring for basic functionality, making it easy to deploy in a variety of environments.

##Contributing
1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Submit a pull request with a detailed explanation of your changes.

##License
This project is licensed under the MIT License.
