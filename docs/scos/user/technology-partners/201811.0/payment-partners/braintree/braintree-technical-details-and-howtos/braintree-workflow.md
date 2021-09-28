---
title: Braintree - Workflow for SCOS
description: This article describes the request flow for the Braintree module in the Spryker Commerce OS.
originalLink: https://documentation.spryker.com/v1/docs/braintree-workflow
originalArticleId: 95ca1fb0-2173-403a-9c9c-f44ebcbd9498
redirect_from:
  - /v1/docs/braintree-workflow
  - /v1/docs/en/braintree-workflow
---

Both credit card and PayPal utilize the same request flow in

* <b>Pre-check</b>: to check the user information to make sure that all the needed information is correct before doing the actual pre-authorization.
* <b>Authorize</b>: to perform a payment risk check which is a mandatory step before every payment. The payment is considered accepted when it is authorized.
* <b>Revert</b>: to cancel the authorization step which cancels the payment before capturing.
* <b>Capture</b>: to capture the payment and receive money from the buyer.
* <b>Refund</b>: to refund the buyer when returning products.
