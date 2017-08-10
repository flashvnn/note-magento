# Magento 2
Note with Magento 2 development


## Generate magento 2 xsd
php bin/magento dev:urn-catalog:generate .idea/misc.xml

## Force run InstallSchema.php 
Run SQL
```sql
delete from setup_module where  module ='module_name';
```
Then run commands:
```
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento cache:clean
```

# Magento 1

## Check magento version
php -r "require 'app/Mage.php'; echo Mage::getVersion(); "

## Fix issue cron.sh: line 54: syntax error: unexpected end of file
sed -i 's/\r$//' cron.sh

## Magento flush email queue recipients
```sql
DELETE 
  FROM `core_email_queue_recipients` 
  WHERE `core_email_queue_recipients`.`message_id` NOT IN 
  (
    SELECT `core_email_queue`.`message_id` 
    FROM `core_email_queue`
  )
```
## Translate

Magento prioritizes translations sources (from highest to lowest):

DB (the core_translate table)
The theme translate.csv file: app/design/frontend/{interface}/{theme}/locale/{lang_ISO}/translate.csv
The app/locale/*/*.csv files

## Remove all url rewrite
Using your favourite database browser, connect to your Magento database

Go to the table named ‘core_url_rewrite’

Empty this table

Log back in to the Magento backend and reindex all

## Reindex 
php shell/indexer.php reindex all

## Run script external

```php
<?php

require_once('app/Mage.php'); //Path to Magento
umask(0);
Mage::app();

// Now you can run ANY Magento code you want

// Change 12 to the ID of the product you want to load
$_product = Mage::getModel('catalog/product')->load(12);

echo $_product->getName();
```

