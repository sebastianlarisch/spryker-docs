---
title: Computop - OMS
description: This article contains information on the state machine commands and conditions for the Computop module in the Spryker Commerce OS.
originalLink: https://documentation.spryker.com/v1/docs/computop-oms-details
originalArticleId: 22ab5611-d105-455b-9afa-30c7610ed3bb
redirect_from:
  - /v1/docs/computop-oms-details
  - /v1/docs/en/computop-oms-details
---

The following plugins are used for performing calls to Paygate during OMS operation.

## Authorize Plugin:
Makes an Authorize call to Computop.

## Cancel Plugin:
Follow these steps to cancel the item in the order in case all the items or the last possible one got canceled:

1. Inquire a call to Computop.
2. Reverse a call to Computop in case Inquire returned "Authorization" was the last action.
3. Change the status of the current item in our DB in case the Inquire call returned that "Authorization" was not the last action. No API calls are needed.
4. If there is any item that is not canceled yet:
  - Change the status of the current item in our DB. No API calls are needed. There is no API call to change the order in Computop.

## Capture Plugin:
Makes a Capture call to Computop.

## Refund Plugin:
Makes a Refund call to Computop.