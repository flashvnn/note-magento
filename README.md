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
The theme translate.csv file
The app/locale/*/*.csv files
