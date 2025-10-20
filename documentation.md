# Chapter 1: Architecture Overview

- Odoo follow a multitier architecture

    - presentation tier
    - logic tier
    - data tier

- Odoo modules

    - collection of functions and data for a specific purpose

# Chapter 2: A New Application

You can create a new module by following these steps:

1. Create a new directory for your module inside the addons path

2. Create the required files:

    A module must contain at least 2 files: the __manifest__.py file and a __init__.py file.

    - __init__.py can be empty

    -  __manifest__.py cannot be empty
        example: https://github.com/odoo/odoo/blob/67a952f30731fc00941587ae165b7a885da0e77e/addons/crm/__manifest__.py

# Chapter 3: Models And Basic Fields

Odoo uses an ORM (Object Relational Mapping) to interact with the database.

To set up a model, follow these steps:

1. Create a models directory inside your module directory.
2. Inside the models directory, create an __init__.py file.
3. Create a Python file for your model (e.g., estate_property.py) and define your model class.
4. Inside your models __init__.py file should import the model files you created.
5. Update your module's __init__.py file to import the models package.

Base model example:

``` python
from odoo import models, fields

class EstateProperty(models.Model):
    _name = 'estate.property'

    name = fields.Char(string='Property Name', required=True)
```

Load module changes by restarting the odoo server with the -u flag followed by the module name.

# Chapter 4: Security - A Brief Introduction

Odoo is a highly data driven system. One way to load data into Odoo is by using CSV files.

By convention, a data file is located in:

    - data folder: importing data
    - security folder: security related data
    - views folder: user interface related data

Every data file has to be declared in the __manifest__.py file of the module.

Example of security/ir.model.access.csv file:

``` csv
id,name,model_id/id,group_id/id,perm_read,perm_write,perm_create,perm_unlink
access_test_model,access_test_model,model_test_model,base.group_user,1,0,0,0
```

# Chapter 5: Finally, Some UI To Play With

As seen in the previous chapters, Odoo is a data driven system. The user interface is no exception to this rule.
Views are defined using XML files.

Actions

    -   Link models to views and menus.
    -   Declared in views and listed in __manifest__.py.

Menus

    -   Defined with <menuitem> elements.
    -   Three levels: root → first level → action menu.
    -   Connect menus to actions for navigation.
    -   Declared in views and in __manifest__.py.

# Chapter 6: Basic Views

List Views

    -   Display records in a table (<list>).
    -   Fields are columns (<field name="field_name"/>).
    -   Tips:
        - Keep unique `id` for each view.
        - Adjust field labels if needed.
        - Check user permissions (Create requires write access).

Form Views

    -   Used to create and edit single records (<form>).
    -   Structure: <sheet>, <group>, <notebook>.
    -   Tips:
        - HTML tags (div, h1) and Odoo classes can be used for styling.
        - Use --dev xml to see changes without restarting the server.

Search Views

    -   Filter and group records (<search>).
    -   Can include <filter> and group_by shortcuts.
    -   Domains (domain) define selection criteria.
    -   Logical operators: & (AND), | (OR), ! (NOT).
    -   Tips:
        - Use XML entities for < and &: &lt; and &amp;.

Domains

    -   Filter records using (field, operator, value) triplets.
    -   Criteria are combined with AND by default.
    -   Allow complex filtering in search views.
