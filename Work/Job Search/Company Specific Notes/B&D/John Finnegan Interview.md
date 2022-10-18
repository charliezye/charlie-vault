[GO BIG](https://www.bdindustrial.com/CoreValues)

-   Need someone with an entrepreneurial/start up mentality with vision for the position and company success.
-   This will be employee #1 internally from an engineering perspective. They would like someone to come in and own the development, but also have strategic vision for the future.
-   All of the development thus far has been done by an external agency (Yonder Agency) and this individual will oversee the external agency, quarterbacking everything as it pertains to B&D Industrial and the OptiPro SaaS Product.
-   They need someone with strong communications skills, poise, and the ability to challenge/make recommendations on technologies to the folks at Yonder Agency, while communicating with leadership, stakeholders, and customers to illicit the correct requirements to improve the product.

###### Rittal 
- Noticed they had IIOT for cooling systems
- What made you leave to come to B&D?

Has Optipro been deployed in many manufacturing facilities yet?

###### Basic about Sensors
- Understand that most have different capabilities to put out different data formats
	- Could be Excel file, JSON, data stream to read from serial port
	- I'm very proficient in handling these different data streams, it's an essential concept for building application backends and programming courses in general!


###### What do you want OptiPro to become?

- What's your long-term vision for the product?
- What's your vision for my involvement and long-term role with the product/future products at your company?
- How much of the future vision of the product will be in my hands?
	- With regards to implementation decisions leading to intended outcomes
	- With regards to internal application architecture/team decisions

###### My Vision (based on limited knowledge)


###### Vision I Present to You

Overall, vision is to provide a secure, scalable, efficient, and comprehensive product that satisfies customer needs first but meets management expectations.

Not to give away the whole farm, but:

1. Device/Actuators
2. Network Layer
	1. Field gateways to pass information from devices to DB
	2. LPWAN, Cellular, Zigbee?
3. AWS Cloud Hosting Solution
	1. Databases:
		1. "Data lake" for all your raw data from sensors
			1. Good if need to analyze data against other data before storing
			2. OR Edge devices 
				1. Store and process data close to its source, only sending a part of the generated records to the data warehouse on the cloud
				3. Can save a lot of time/resources otherwise used to send raw data to cloud
		2. "Cloud gateways" for compression and entry of important information to cloud
			1. Transform, filter, and aggregate data before sending to data warehouse, e.g. changing formatting
		3. "Data warehouse" to store insightful data
		5. Data analytics in AWS and in backend to analyze issues/bugs in process
		6. Caching with Elasticache, Cloudfront, Route 53
4. Whichever backend framework you're using
	1. All your complex data querying and analytics for data used in visualizations and presentation to users
	2. Django most likely, consider Java and NodeJS as well
6. Angular Frontend for user applications/touchpoints
7. Long term: 
	1. Machine learning to customize functionalities, analyze devices, and extract big data trends across customers
	2. Not sure if this is applicable, but use of smart phones, smart watches or other wearables for workers
		1. These have a ton of sensors built in and I've worked with them between Ubiquitous Computing and work w/ Ware2Go

Why is this plan important?
1. Maintainability
2. Scalability
3. Cost-efficiency
4. High/quick performance
5. Interoperability
6. Security
How does it accomplish this?
- Microservices, modularization
- Clear division of labor among steps and prioritization of important data
- No storage of parts that are not useful
