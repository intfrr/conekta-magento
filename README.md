conekta-magento
==============

Magento Version Compatibility
-----------
The plugin has been tested for Magento 1.7 and 1.8. Conflicts can be found if installed in non tested Magento versions.

Installation
-----------

  * If you are using a checkout different from Magento's default, be sure that /js/Conketa/conekta_pm_logic.js is set properly. It uses payment.save() function and payment-buttons-container div which are used in Magento's default template. Change them accordingly to the checkout of your preference.

````// Depending on the checkout, buttonAction and button must be changed

var buttonAction = function() {
payment.save();
};````

`// This is the button that saves the payment method, or completes the checkout if it has only one step.`

`var button = $(":button[onclick='payment.save()']");`  

  * If your Magento installation does not have JQuery, add to your page.xml the following lines before prototype is defined:

`<action method="addItem"><type>js</type><name>Conekta/jquery.js</name></action>`

`<action method="addItem"><type>js</type><name>Conekta/jquery-ui.js</name></action>`
  * Copy the folder and paste it in the folder where you have installed Magento.
  * In the Magento admin, navigate to 'System-Cache Management'. Select and disable all Cache Types.  Additionally, click "Flush Magento Cache" and "Flush Cache Storage".  These steps will allow you to start testing the plugin.
  * In the 'System->Configuration' section, click the 'Payment Methods' link in the left hand navigation.  Check that the payment methods "Pago con Tarjeta de Débito / Crédito", "Pago con Oxxo" and "Pago con Transferencia Bancaria" appear. If these payment methods do not show up, check that your magento user has priviledges to access the Magento folder.
  * Each of the payment methods should should 'Enabled'=>'Yes', in the 'Api Keys' section for the payment methods paste the api keys found in https://admin.conekta.io#developers.keys, e.g.
    
Api Public Key: 
    `key_KJysdbf6PotS2ut2`
Api Private Key: 
    `key_eYvWV7gSDkNYXsmr`


You will also need to configure payment notifications for your server.  Within https://admin.conekta.io#developers.webhooks, create a new url which points to your server.
If your server has mod_rewrite enabled, the url for your webhook will be:
    `http://mydomain.com/invoice/ajax/listener`
Otherwise, your url for your webhook will be:
    `http://mydomain.com/index.php/invoice/ajax/listener`
After having completed these steps the payment methods should be enabled for testing.

Inventory Notes
---------------

Your product inventory will only be adjusted when your server receives a payment notification from Conekta, this allows for offline payment methods like Bank Deposits and Oxxo to be processed.

Dependency Notes
-----------

Included modules for the plugin include:
  * Conekta_Bank
  * Conekta_Oxxo
  * Conekta_Card
  * Conekta_Invoice

The Conekta_Invoice must be enabled because it handles credit card tokenization logic.
