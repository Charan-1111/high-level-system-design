# Disaster Recovery
- Disaster Recovery ( DR ) is the process, strategy, and set of mechanisms designed to restore critical systems, data and operations after a disruptive event - such as hardware failure, natural disaster, cyber attack or human error.
- Goal of DR is to minimize downtime and data loss and ensure that business operations can resume as quickly as possible after a disaster.
- Disaster Recovery Plan - Portfolio of policies, tools and processes used to recover or continue operations of critical IT infrastructure, systems and software after a natural or human-made.

- ## Types of Disasters
	- Natural :- Earthquakes, floods, fires, hurricanes.
	- Technical :- Hardware failure, software bugs, data corruption.
	- Human :- Accidental deletion, configuration errors.
	- Cyber :- Ransomware attacks, DDos, data breaches.
	- Infrastructure :- Power outages, network failures, ISP failures.

- ## Importance of disaster recovery
	- Protects data :- Minimizes data loss and ensures quick recovery.
	- Ensures business continuity :- Allows operations to resume quickly after a disruption.
	- Reduces financial impact :- Minimizes revenue loss, fines and recovery costs.
	- Maintains reputation :- Protects brand image and customer trust.
	- Meets compliance requirements :- Helps adhere to data privacy laws and industry standards.

- ## Key Metrics in Disaster Recovery
	- Two critical metrics define the effectiveness of DR plan.
	1. **Recovery Point Objective**
		- Maximum acceptable amount of data loss measured in time.
		- Or the maximum age of data we need to recover to resume operations after a major event.
		- It helps to define the frequency of data backups.
	2. **Recovery Time Objective**
		- Maximum acceptable downtime after a disaster without causing significant damage to the business.
		- Eg :- Some applications/services can be down for an hour, but some need to be recorded in minutes.

- ## Disaster Recovery Strategies
	1. **Backup and Restore**
		- Data is backed up periodically to local or cloud storage.
		- In a disaster systems are rebuilt and data is restored from backups.
		- Pros :- Simple, inexpensive
		- Cons :- Slow recovery, large RPO & RTO.
	2. **Pilot Light**
		- A minimal version of the system runs in another region or cloud.
		- In a disaster, additional resources are started to scale it up.
		- Pros :- Faster recovery than backup.
		- Cons :- Slightly more cost due to minimal live setup.
	3. **Warm Standby**
		- A scaled-down but continuously running copy of the system is maintained.
		- Can quickly scale up to full capacity during a disaster.
		- Pros :- Faster failover.
		- Cons :- Higher Cost.
	4. **Active-Passive**
		- Primary site handles all traffic, secondary ( passive ) site is synchronized but idle.
		- On disaster traffic switches to passive site.
		- Pros :- Quick recovery.
		- Cons :- Expensive to maintain duplicate resources.
	5. **Active-Active**
		- Two or more geographically distributed sites actively handle traffic simultaneously.
		- If one fails, other continue seamlessly.
		- Pros :- Almost zero downtime, lowest RTO/RPO
		- Cons :- Most expensive, requires strong synchronization and load balancing.

- ## Components of DR Plan
	- A well-defined DR Plan includes.
	1 . Risk assessment :- Identify potential threats and vulnerabilities that could disrupt the systems and business operations.
	2 . Critical System Inventory :- Classify what's mission-critical.
	3 . Data backup strategy :- Frequency storage and retention policy.
	4 . Failover and Fallback procedures :- How to switch to backup systems and return.
	5 . Communication Plan :- Notify teams, customers and stakeholders.
	6 . Testing Schedule :- Regular DR drills and simulations.
	7 . Documentation :- Step-by-step recovery procedure.
