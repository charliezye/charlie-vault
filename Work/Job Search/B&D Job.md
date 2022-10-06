# B&D Industrial Job Notes

- IIOT: Industrial Internet of Things

#### Optipro
- Gathers data in 5 most common coding languages and combines into cohesive dashboard

How old is the OptiPro product now?
- Saw that TM was filed in August

##### About the Application
###### Steps
1. Connect IIOT devices
2. Gather and translate data into one unified dashboard
	1. Internet browser
2. Optimize data into one user interface with various views
	1. Data visualization techniques
2. Custom reporting/alerts
	1. Power BI, Tableau, Google Data Studio''

###### Features:
1. Remote Monitoring from Any Internet Connection
2. Optimize Throughput with Smarter Resource Allocation
3. Efficiently Capture Data from Multiple Devices
4. Simple Dashboard and Graphics
5. Export Data easily for Advanced Analysis

>>Faster throughput, higher efficiency, reduced operational costs, and less waste

#### Questions about OptiPro

**What kind of production machines interacting with?**
- Listed by OptiPro press release
	- Industrial Measuring Devices
	- Microcomponents
	- Electrical products
	- Identification products
	- Industrial weighing
- Programmable Logic Controller (PLC)
	- Ladder logic
- Process Automation Controller (PAC)
	- FPGA
	- Decentralized, able to connect to remote input/output (I/O) and other PACs
- Industrial PC
	- OS like Windows/Linux

**What languages do production machines use?** 
- C, C++, Python, Java?
- G-Code, M-Code, CAM?
- Proprietary?

##### What do you want OptiPro to become?

- What's your long-term vision for the product?
- What's your vision for my involvement and long-term role with the product/future products at your company?
- How much of the future vision of the product will be in my hands?
	- With regards to implementation decisions leading to intended outcomes
	- With regards to internal application architecture/team decisions

###### Now: Unstructured set of individual codes/scripts

###### What does this entail?
- Saw on rebranding press release that it is labeled as cloud-based, on-premises, or hybrid-cloud platform
	- Are there already some cloud capabilities? 

**Currently sell/install this software with 4-5 hours**
- Who sells/installs? Company employee or Yonder Group?
- How involved is this process?
- How much difference between customers, any way to more easily streamline?
- Is there data your company collects from individual customers that can be used for internal analysis/improvements?

**Script chosen based on device to aggregate code/data?**
- How involved is this process? How much code is in each script?
- How has Blue Yonder set you up for transitional success?
	- Is there already internal documentation on the application?
- How does your pipeline/architecture look right now?
	- Django Model View Template (MVT)
- What's the backend built in?
	- Java and Node.js are generally faster than Python
		- During compilation are generally faster due to not dynamic typing
		- Up to 10x faster
	- Java has much faster performance
		- 10x+ less CPU seconds for Java/Node.js vs. Python
		- On Amazon servers, EC2 pricing is based around compute capacity so this would save a lot of money
	- These play a big role in scalability as codebase grows
- Is the goal microservices? API pipelines?
	- Is there any machine learning you plan to/are already involving?

**Is data stored on local database servers right now?**
- How is data collected from machines and sent to server?
- How is data queried and returned to application?
- Is there any caching currently involved with Redis or other frameworks?
	- Seems like high throughput, want fast response/low latency
	- Lot of old data to display that doesn't need to be re-queried
	- Session store

**Measuring Efficiency of App**
- How has efficiency of application itself been measured internally?
	- Runtime of queries, time to load page/data visualizations, etc.
- How is ROI measued?

###### Outcome: MVP to launch into marketplace

**Clearly want cloud-based solution**
- Why was this not originally built on the cloud/with "box" around services?
	- Was use proprietary at first?

**Why did you choose to create OptiPro as a software solution to sell to other companies?**
- Will this compete with other SAAS platform solutions in your industry?
- Any difficulties with adapting to certain machinery or issues selling to companies with proprietary IIOT SAAS? What is the plan to set this application apart?
- Market analysis?

**What's the scope of this first endeavor? Timeline?**
- Is timeline to MVP 6-7 months? 
- How much additional work will be involved with implementing application from current state to cloud state?
- Is it just translating to microservices and hosting on the cloud?
- Are there new features?
- What plans for working to move away from Blue Yonder and build own team?
	- Timeline?

###### Vision I Present to You

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
4. Transition to Express Node.JS backend
	1. All your complex data querying and analytics for data used in visualizations and presentation to users
	2. Node.js is great for IoT because forces you to build asynchronous I/O
		1. Programs permit other processing to continue (non-blocking) before data is returned to frontend
		2. Essentially in sychronous, you tell worker instructions, they leave, finish the work, then come back with the work before starting next set
		3. Asynchronous has a middle-man called an event handler passing on instructions to multiple workers at once and returning their work, making it very memory efficient
	3. Already using JS for frontend so just makes sense
6. Angular Frontend for user applications/touchpoints
7. Long term: Machine learning to customize functionalities, analyze devices, and extract big data trends across customers

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

###### Backend Architecture Examination
1. Django MVT
	- Like MVC but template instead of view and view instead of controller
	1. Model
		1. SQL DB
	2. View
		1. Takes web requests, returns web response
		2. Render HTML/CSS/JS into what you see on web page 
		3. Equivalent of Controller in MVC
	4. Template
		1. Static parts of HTML and dynamic content
		2. Equivalent of view in MVC

#### Culture Fit Questions
- Who will I primarily be communicating with to meet needs (who is my top priority client)
	- I assume I am building a product to the specifications of the companies buying it and your company management
	- How will I be assisted in developing management vision into product that also meets needs of customers? 
	- Do you anticipate any particular vision concerns/conflicts that may arise?

##### Industries/Products B&D Serve
"Bearing Supplier"
###### Gearbox Solutions
- Reducer repair
- Root cause failure
	- Engineer assessment of application
- Field service
>> gearing, bearings, reducers, drive shafts, and couplings and how they relate to machine performance

###### MRO + Automation Solutions
- Start with static load, work thrtough kientics
- Automation solutions
	- AC/DC drives
- Bearings and Power Transmission solutions
	- Certified bearing experts fit machine goals/specifications
- Material Handling Solutions
- Custom bulk material handling solutions
	- High production needs
	- Complete mechanical/automation solutions
	>> **screw, drag, and belt conveyors,** as well as bucket elevators
- MRO Solutions
	- Maintenance, repair, operations
	- Bearings
	- Seals
	- Belts
	- Motors
	- VFDs
	- Sensors
	- Gearing

##### Blue Yonder
- Mission: 
	- To empower every person and organization to fulfill their potential
	- "Innovative, AI-driven supply chain platform"
	- Comprehensive supply orchestration (E2E)
- B&D not listed as a customer?