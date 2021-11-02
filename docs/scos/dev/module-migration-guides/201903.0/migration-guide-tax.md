---
title: Migration Guide - Tax
last_updated: Nov 22, 2019
template: module-migration-guide-template
originalLink: https://documentation.spryker.com/v2/docs/mg-tax
originalArticleId: a080ccf1-a49d-45c8-b8e6-77c020a5b0d6
redirect_from:
  - /v2/docs/mg-tax
  - /v2/docs/en/mg-tax
related:
  - title: "Reference information: Tax module"
    link: docs/scos/dev/feature-walkthroughs/page.version/tax-feature-walkthrough/reference-information-tax-module.html
---

## Upgrading from Version 4.* to Version 5.*

In version 5, tax calculation logic changed, tax amount for options, expenses and items are now calculated in the Tax module. 
The plugins: `ExpenseTaxCalculatorPlugin`, `ItemTaxCalculatorPlugin` and `TaxTotalsCalculatorPlugin` were removed, and replaced with:

* `TaxAmountCalculatorPlugin` - to calculate item, item product option and expense taxes. 
* `TaxAmountAfterCancellationCalculatorPlugin` - to calculate tax amount after cancellation/refund happened.

Corresponding plugin business classes, `ExpenseTaxCalculator`, `ItemTaxCalculator`, `TaxCalculation` were also removed and replaced with:
* Business classes `TaxAmountCalculator` 
* `TaxAmountAfterCancellationCalculator` 

## Upgrading from Version 2.* to Version 3.*

If you’re migrating the Tax module from version 2 to version 3, you need to follow the steps described below.
With the version 3 of the Tax module, new tax calculation is used. The tax rate is based on the current shipping country or, if it’s unavailable, a default tax rate value is used.
First you need to execute a database schema migration:
```sql
ALTER TABLE "spy_tax_rate"
ADD "fk_country" INTEGER;
ALTER TABLE "spy_tax_rate" ADD CONSTRAINT "spy_tax_rate-fk_country"
   FOREIGN KEY ("fk_country")
   REFERENCES "spy_country" ("id_country");

ALTER TABLE "spy_tax_rate"
 ADD "created_at" TIMESTAMP,
 ADD "updated_at" TIMESTAMP;

ALTER TABLE "spy_tax_set"
 ADD "created_at" TIMESTAMP,
 ADD "updated_at" TIMESTAMP;
 ```
 
Now you should be able edit the tax rates in Zed, under the tax section.
To use the new tax rate calculation logic, you need to register the tax calculator plugins in `CalculationDependencyProvider::getCalculatorStack()`:
`ItemTaxCalculatorPlugin` - used after item sum gross amounts are calculated.
`ShipmentTaxRateCalculatorPlugin` - used after expense gross sum amount is calculated.
`ProductOptionTaxRateCalculatorPlugin` - used after item sum gross amounts are calculated.
`ProductItemTaxRateCalculatorPlugin` - used after item sum gross amounts are calculated.
`ExpenseTaxCalculatorPlugin` - used after expense gross sum amount is calculated.

If you have discounts:

* `ItemsWithProductOptionsAndDiscountsGrossPriceCalculatorPlugin()` - after `SumGrossCalculatedDiscountAmountCalculatorPlugin`.
* `ItemsWithProductOptionsAndDiscountsTaxCalculatorPlugin()` - after `ItemsWithProductOptionsAndDiscountsGrossPriceCalculatorPlugin`.
* `DiscountTotalsWithProductOptionsCalculatorPlugin` - after `DiscountTotalsCalculatorPlugin`.
* `ExpenseTaxWithDiscountsCalculatorPlugin` - after `DiscountTotalsWithProductOptionsCalculatorPlugin`.
* `TaxTotalAmountWithProductOptionsAndDiscountsCalculatorPlugin` - after `TaxTotalsCalculatorPlugin`.

<!--**See also:**
Get a general idea about Tax Module-->