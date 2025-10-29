# Circuit Breakers
- A Circuit breaker is a software design pattern used to detect failures and prevent an application from repeatedly trying an operation that is likely to fail.

- ## Need for Circuit Breakers
	- In a microservice architecture, one service often depends on many other services.
	- If one service is slow or down, and other services keeps calling in repeatedly, following issues araises
		- Requests pile up -> Thread pool exhaustion
		- More retries -> Increased latency.
		- Failure Spreads -> Cascading Failures.
		- Entire System slowdown or crashes.

- Circuit breaker has three main states.
	- Closed -> Everything is normal, all requests pass through. Failures are counted.
	- Open -> Too many failures occured. The breaker "trips"- no calls allowed. Calls fail immediately.
	- Half-open -> After a timeout, a few trail requests are allowed. If successful, the breaker closes again; if not it reopens
