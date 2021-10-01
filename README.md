# infrared - get-cust-segmentation

Infers the type of customer based on input

![infrared](mouse.PNG)

### What is `htdc`?
Hybrid Tree Dynamic Clustering

### What does `htdc` do?
Customer classification and inference

- `htdc` can be used for model training, adhoc clustering and exploratory analysis
- `htdc` can be embedded in code for operationalized analysis and customer segmentation inference

## Structure
- `lambda_function.py` - invokes infrared to infer the customer type
- `infrared.py` - infers customer type using an `htdc` model

### Request
- dict
	- model_srn ([srn](https://wiki.sabrenow.com/display/SPT/Athena+SRN))
	- params (dict)
		- adults (int)
		- arrivaldate (str)
		- arrivaldate_weekday (str)
		- children (int)
		- leaddays (int)
		- lengthofstay (int)

Example:
```
{
 'model_srn':'srn:amazon:aws:::file:models/default/rule_based_clustering.pickle,
 'params': {
	'Adults': 2, 
	'Children': 0, 
	'LeadDays': 11, 
	'LengthOfStay': 2, 
	'ArrivalDateWeekDay': 'friday'}
}
```

### Response
- dict
	- status_code (int):
	- data (dict)
		- segmentation_result (tuple): segmentation results
		- response_metadata (dict):
			- model_hash (hash): md5 hash of model used
			- model_srn (srn): location of model used
			- request_id (uuid): unique identifier
			- timestamp (datetime): timestamp of request

Example:

```{'status_code': 200,
 'data': {
	'segmentation_result': ('personaltimeoff', 1.0),
	'response_metadata': {'model_hash':'07d96ee48766095795941cda5492f2fa',
                          'model_srn': 'srn:amazon:aws:::file:models/default/rule_based_clustering.pickle',
                          'request_id': 'c0c54a12-b370-4611-bea6-271e41501d54',
                          'timestamp': '2020-04-04 20:23:57.107931'}
          }
```










