# IlliadShippingNotificationAddon



This is an ILLiad server addon which does a few things when a lender marks a loan request "shipped." Specifically, it looks for loan requests in a status of Request Sent which have a due date defined - this is as good a proxy for the OCLC status update as currently exists.

This version of the addon has been modified to suit specific needs at the University of Maryland, College Park, and may not be suitable for general use. The general-use version is available at https://github.com/austinfsmith/IlliadShippingNotificationAddon

When shipped requests are found, the addon does the following:

1. Updates an ItemInfo field with a "Shipped on <date>" message. The idea is that this field will be displayed in the Outstanding Requests table in the patron's ILL account.

2. Sends an email notification to the patron, letting them know that the item has shipped.

3. If the request has a DocumentType of "EBook", changes it to "Book". This forestalls a common source of confusion for patrons at UMC.

4. If the request has a loan period of less than 8 weeks, adds a warning note to the Special Instructions field. The idea is that this field will be included on the loan labels printed later, to forewarn the patron about the short loan period.

## Configuration

The addon has the following settings:

DeferProcessing - If set to True, the addon will not check any requests until 11PM local time. This should give some time for items mistakenly marked Shipped to be caught & corrected before an erroneous email is sent.

SendEmail - If set to False, no email will be sent (but the shipment date will still be added to the field defined in ItemField).

EmailName - Name of the email template to send. This must be defined in the Customization Manager. The same email will be sent for all requests (regardless of where they're coming from), so you'll want to be careful with the wording.

ItemField - Name of the field in the Transactions table to store the shipment date in. This exists so that these dates can be displayed in the Outstanding Requests table in the patron's ILL account, if desired.

AddShortLoanPeriodNote - If true, a message will be added to Special Instructions for items with short due dates.

ShortLoanPeriod - Defines the loan period which will trigger the ShortLoanPeriodNote

ShortLoanPeriodNote - Text that will be added to the Special Instructions field for items with short loan periods.
