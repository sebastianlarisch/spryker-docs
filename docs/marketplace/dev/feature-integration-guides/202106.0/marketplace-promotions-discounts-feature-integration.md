---
title: Marketplace Promotions & Discounts feature integration
last_updated: Jan 04, 2021
description: This document describes the process how to integrate the Marketplace Promotions & Discounts feature into a Spryker project.
template: feature-integration-guide-template
---

This document describes how to integrate the Marketplace Promotions & Discounts feature into a Spryker project.

## Install feature core

Follow the steps below to install the Marketplace Promotions & Discounts feature core.


### Prerequisites

To start feature integration, integrate the required features:

| NAME | VERSION | INTEGRATION GUIDE |
| - | - | - |
| Spryker Core                 | 202001.0   | [Spryker Core feature integration](https://documentation.spryker.com/docs/spryker-core-feature-integration) |
| Marketplace Order Management | dev-master | [Marketplace Order Management feature integration](/docs/marketplace/dev/feature-integration-guides/{{ page.version }}/marketplace-order-management-feature-integration.html) |
| Promotions & Discounts       | 202001.0   | [Promotions & Discounts feature integration](https://github.com/spryker-feature/promotions-discounts) |

###  1) Install the required modules using Composer

Install the required modules:

```bash
composer require spryker-feature/marketplace-promotions-discounts --update-with-dependencies
```

{% info_block warningBox "Verification" %}

Make sure that the following modules were installed:

| MODULE | EXPECTED DIRECTORY |
| - | - |
| DiscountMerchantSalesOrder    | spryker/discount-merchant-sales-order     |
| DiscountMerchantSalesOrderGui | spryker/discount-merchant-sales-order-gui |

{% endinfo_block %}

### 2) Set up the transfer objects

Generate transfer changes:

```bash
console transfer:generate
```

{% info_block warningBox "Verification" %}

Make sure that the following changes were applied in transfer objects:

| TRANSFER  | TYPE  | EVENT | PATH |
| - | - | - | - |
| MerchantOrder.merchantOrderItems | attribute | created | src/Generated/Shared/Transfer/MerchantOrderTransfer |

{% endinfo_block %}

### 3) Zed translations

Generate a new translation cache for Zed:

```bash
console translator:generate-cache
```

### 4) Set up configuration

Change the following the configuration to enable the feature:

| CONFIGURATION | SPECIFICATION | NAMESPACE |
| - | - | - |
| MerchantSalesOrderMerchantUserGuiConfig   ::getMerchantSalesOrderDetailExternalBlocksUrls | Adds Merchant discount separation while viewing Merchant Order. | \Pyz\Zed\MerchantSalesOrderMerchantUserGui\MerchantSalesOrderMerchantUserGuiConfig |

**src/Pyz/Zed/MerchantSalesOrderMerchantUserGui/MerchantSalesOrderMerchantUserGuiConfig.php**

```php
<?php

namespace Pyz\Zed\MerchantSalesOrderMerchantUserGui;

use Spryker\Zed\MerchantSalesOrderMerchantUserGui\MerchantSalesOrderMerchantUserGuiConfig as SprykerMerchantSalesOrderMerchantUserGuiConfig;

class MerchantSalesOrderMerchantUserGuiConfig extends SprykerMerchantSalesOrderMerchantUserGuiConfig
{
    /**
     * @return string[]
     */
    public function getMerchantSalesOrderDetailExternalBlocksUrls(): array
    {
        return [
            'discount' => '/discount-merchant-sales-order-gui/merchant-sales-order/list',
        ];
    }
}
```

### 5) Set up behavior

Enable the following behaviors by registering the plugins:

| PLUGIN | DESCRIPTION | PREREQUISITES | NAMESPACE |
| - | - | - | - |
| DiscountMerchantOrderFilterPlugin | Removes none merchant-related discounts from merchant orders. |           | Spryker\Zed\DiscountMerchantSalesOrder\Communication\Plugin |

**src/Pyz/Zed/MerchantSalesOrder/MerchantSalesOrderDependencyProvider.php**

```php
<?php

namespace Pyz\Zed\MerchantSalesOrder;

use Spryker\Zed\DiscountMerchantSalesOrder\Communication\Plugin\DiscountMerchantOrderFilterPlugin;
use Spryker\Zed\MerchantSalesOrder\MerchantSalesOrderDependencyProvider as SprykerMerchantSalesOrderDependencyProvider;

class MerchantSalesOrderDependencyProvider extends SprykerMerchantSalesOrderDependencyProvider
{
    /**
     * @return \Spryker\Zed\MerchantSalesOrderExtension\Dependency\Plugin\MerchantOrderFilterPluginInterface[]
     */
    protected function getMerchantOrderFilterPlugins(): array
    {
        return [
            new DiscountMerchantOrderFilterPlugin(),
        ];
    }
}
```

---


{% info_block warningBox "Verification" %}

Make sure that correct discounts are applied to the merchant orders when viewing them in the Back Office.

{% endinfo_block %}