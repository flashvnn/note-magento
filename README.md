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
