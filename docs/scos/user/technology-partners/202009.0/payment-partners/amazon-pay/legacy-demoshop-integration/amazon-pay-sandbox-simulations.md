---
title: Amazon Pay - Sandbox Simulations
description: In this article, you can get information about sandbox simulations for the Amazon Pay module in Spryker Legacy Demoshop.
originalLink: https://documentation.spryker.com/v6/docs/amazon-pay-simulations-demoshop
originalArticleId: 90d60020-ff45-4958-8dd3-5471b776c15f
redirect_from:
  - /v6/docs/amazon-pay-simulations-demoshop
  - /v6/docs/en/amazon-pay-simulations-demoshop
---

In order to reproduce some edge cases like declined payment or pending capture, Amazon provides two solutions. The first is special methods marked with a red star on payment widget.

![Click Me](https://spryker.s3.eu-central-1.amazonaws.com/docs/Technology+Partners/Payment+Partners/Amazon+Pay/amazon_payment_widget.png)
It allows reproducing different cases of `decline` payment workflow.

But there are more edge cases like expired authorization or pending capture for which there is only one way to reproduce - pass simulation string as `SellerNote` parameter of API request.