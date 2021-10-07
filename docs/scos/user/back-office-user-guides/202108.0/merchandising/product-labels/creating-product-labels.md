---
title: Creating product labels
description: Back Office guide for creating product labels.
originalLink: https://documentation.spryker.com/2021080/docs/creating-product-labels
originalArticleId: fddd9b4b-1aec-473d-922d-e56f7040ee2e
redirect_from:
  - /2021080/docs/creating-product-labels
  - /2021080/docs/en/creating-product-labels
  - /docs/creating-product-labels
  - /docs/en/creating-product-labels
---

This topic describes how to create and activate product labels.

## Prerequisites

To start working with product labels, go to **Merchandising** > **Product Labels**.

Review the reference information before you start, or just look up the necessary information as you go through the process.

## Creating product labels

To create a product label:
1. On the *Overview of Product Labels* page, select **Create Product Label**.
2. In the *General* section of the *Create a Product Label* page, do the following:
    1. enter:
    * **Name**
    * **Front-end Reference**
    * **Priority**
    2. If you want to activate the product label, select **Is active**.
3. In the *Behavior* section, select:
    * **Valid From** and **Valid to** dates.
    * **Is exclusive** if you want the product label to be exclusive.
4. In the *Store relation* section, select stores in **Select Stores**.

{% info_block infoBox %}

Even if there is only one store in your shop, you still need to select it for the product label to be displayed on the Storefront.

{% endinfo_block %}

5. In the *Translations* section, enter **Name** for all the locales.
See [Product Label: References](https://documentation.spryker.com/2021080/docs/product-labels-reference-information) to learn about the attributes on this page.
6. Switch to the *Products* tab.
7. In the *Select* column, select one or more products to assign the label to. 

{% info_block warningBox %}

Make sure the selected products are listed in the *Selected products to assign ({number of products})* tab.

{% endinfo_block %}

8. Click **Save**.
The page refreshes to display the success message about product label creation.

**Tips & tricks**
* Below the table, click **Select All** to assign the label to all the products in the *Available products* tab.
* Filter the products in the *Available products* tab by entering its name, SKU, or category name in the **Search** field.
* In the *Selected* column of the *Selected products to assign ({number of products})*, click **Remove** to remove a selected product.

### Reference information: Creating product labels 

The following table describes the attributes you see, select, or enter while creating and editing a product label in the Settings tab.

| ATTRIBUTE | DESCRIPTION |
| --- | --- |
| Name | Name of the product label. |
| Front-end Reference | Defines the location and design of the product label. By default, the following designs are available: *alternative*, *discontinued*, *top*, *new*, *sale*. |
| Priority | Defines the order in which labels will appear on a product card and product details page. The product label with the lowest number will have the highest priority. |
| Is active | Check box that, if selected, defines that the product label is active.  |
| Valid from and Valid to | Inclusively defines the time period when the product label will be displayed. If no dates are selected, the label is always displayed. |
| Is exclusive | Check box that defines the product label exclusivity. If an exclusive product label is applied to a product, all the other applied product labels will not be displayed on the product card. |
| Select Stores | Stores in which a product label will be visible and available on the Storefront. |
| Name in the *Translations* section | Name of the product label translated to a respective language. |


In the *Products* tab, you can see the following information:

* Autogenerated product ID
* Product SKU
* Product name
* The categories the product label is assigned to
* Product price
* Product status

In the *Products* tab, you can do the following:

* View a product
* Sort by ID, SKU, and Name
* Search by SKU and Name

**What's next?**

* To learn how to edit product labels, see [Editing Product Labels](/docs/scos/user/back-office-user-guides/{{page.version}}/merchandising/product-labels/managing-product-labels.html#editing-product-labels).
* To learn how you can manage product labels, see [Managing Product Labels](/docs/scos/user/back-office-user-guides/{{page.version}}/merchandising/product-labels/managing-product-labels.html).
