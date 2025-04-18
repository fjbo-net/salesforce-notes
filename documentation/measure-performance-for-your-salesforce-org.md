# Measure Performance for Your Salesforce Org

🔗 Source: [Salesforce Help](https://help.salesforce.com/s/articleView?id=xcloud.technical_requirements_measuring_ept.htm&type=5)

## Key Takeaways 🧠

- **Performance**: Speed and effectiveness under a given workload and timeframe

- **Scalability**: System's ability to maintain response time/throughput as demands increase

- [Key Steps for Performance Testing](#1-key-steps-for-performance-testing)

	1. [Planning and Setup](#1-1-planning-and-setup)

	0. [Persona Identification](#1-2-persona-identification)

	0. [Performance Measurement Methods](#1-3-performance-measurement-methods-ept---experienced-page-time)

	0. [Testing Considerations](#1-4-testing-considerations)

## 1. Key Steps for Performance Testing

### 1. 1. Planning and Setup

&uarr; [Key Steps for Performance Testing](#1-key-steps-for-performance-testing)

1. Use a full-copy sandbox that mirrors production data model
0. Create a system diagram showing current/future features and systems
0. Calculate system throughput in Requests per Second (RPS)
0. Map out data volumes and relationships
0. Note: Sandbox performance isn't indicative of production performance due to different hardware/instances


### 1. 2. Persona Identification

&uarr; [Key Steps for Performance Testing](#1-key-steps-for-performance-testing)

1. Different roles have varying data visibility and volumes

	- Example: VP of Sales vs specialized roles

0. Create site maps and page flows for each key persona


### 1. 3. Performance Measurement Methods (EPT - Experienced Page Time)

&uarr; [Key Steps for Performance Testing](#1-key-steps-for-performance-testing)

1. Add EPT counter to app header (using `?eptVisible=1` or Debug Mode)
0. Use Lightning Usage App for browser/page performance
0. Create custom reports using Lightning Usage App objects (not available in sandbox org)
0. Utilize Event Monitoring Analytics App


### 1. 4. Testing Considerations

&uarr; [Key Steps for Performance Testing](#1-key-steps-for-performance-testing)

1. Measure browser octane score and network latency first
0. Run tests multiple times to eliminate variance
0. Test regularly and track changes
0. Use tools like LoadRunner or JMeter for load testing
0. Consider using Selenium for page flow performance
0. Use browser developer tools for network throttling