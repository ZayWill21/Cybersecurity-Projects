# Secure Cloud: Enabling AWS Security Hub Enhanced Capabilities

![AWS](https://img.shields.io/badge/AWS-Security%20Hub-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![GuardDuty](https://img.shields.io/badge/Amazon-GuardDuty-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Inspector](https://img.shields.io/badge/Amazon-Inspector-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Security](https://img.shields.io/badge/Security-CSPM-green?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-blue.svg?style=for-the-badge)

## Overview

This project delivers a comprehensive implementation of AWS Security Hub's enhanced capabilities, demonstrating enterprise-grade security orchestration and automated response capabilities across multi-account AWS environments. The implementation showcases Security Hub's advanced correlation engine, which aggregates and prioritizes security signals from multiple AWS-native security services including GuardDuty, Inspector, Macie, and Security Hub CSPM to provide unified visibility into threats, vulnerabilities, misconfigurations, and data exposure risks.

Built with a cloud support engineering perspective, this addresses the critical challenge of security alert fatigue and fragmented tooling that plagues modern cloud operations teams. By leveraging the Open Cybersecurity Schema Framework (OCSF) for data normalization and implementing intelligent finding correlation, the solution enables security teams to identify attack paths, assess blast radius, and prioritize remediation efforts based on actual exploitability rather than theoretical risk scores. The architecture demonstrates how organizations can achieve comprehensive security visibility while maintaining operational efficiency through centralized management via AWS Organizations and delegated administration patterns.

Please note that some information was redacted for security concerns

## Features / Key Accomplishments

- **Multi-Service Security Orchestration**: Integrated five AWS security services (GuardDuty, Inspector, Security Hub CSPM, Macie, and Security Hub) into a unified security operations platform with centralized finding management
- **OCSF-Based Data Normalization**: Implemented Open Cybersecurity Schema Framework standardization enabling seamless integration with SIEM platforms and third-party security tools
- **Exposure Finding Correlation**: Demonstrated advanced correlation capabilities identifying network-exploitable vulnerabilities with potential remote execution paths and blast radius visualization
- **Attack Path Visualization**: Validated Security Hub's ability to map multi-hop attack chains combining misconfigurations, vulnerabilities, and network exposures into actionable security insights
- **Optimized Trial Period Management**: Strategically coordinated service activation across GuardDuty (30-day), Inspector (15-day), Macie (30-day), and CSPM (30-day) trials to maximize evaluation coverage
- **Organization-Wide Deployment**: Configured delegated administrator pattern for centralized security management across AWS Organizations with multi-region support
- **Automated Ticketing Integration**: Established bidirectional integration with enterprise ITSM platforms (Jira Cloud/ServiceNow) for automated incident workflow management
- **Comprehensive Finding Categorization**: Implemented classification framework spanning Compliance, Data Security, Detection, Vulnerability, and Exposure finding types
- **Validated Threat Detection**: Utilized AWS Labs GuardDuty Findings Tester to generate realistic security events and validate end-to-end detection and correlation pipelines
- **Resource Inventory Integration**: Leveraged Security Hub's configuration aggregation to maintain real-time asset inventory with security context enrichment

## Architecture

The Secure Cloud implements a hub-and-spoke security architecture leveraging AWS Organizations for centralized management. Security Hub operates as the central aggregation and correlation layer, ingesting findings from distributed security services across multiple accounts and regions. The delegated administrator pattern enables security teams to maintain separation of duties while providing comprehensive visibility into the security posture of member accounts. GuardDuty provides runtime threat detection, Inspector performs continuous vulnerability and network reachability assessments, Macie discovers and classifies sensitive data, and Security Hub CSPM evaluates compliance against industry frameworks. All findings are normalized using OCSF and correlated to identify exposure paths, with critical findings automatically routed to ITSM platforms for incident response workflows.

<!-- INSERT ARCHITECTURE DIAGRAM HERE -->

**Recommended Diagram**: A multi-layer architecture diagram showing:
1. **Top Layer**: AWS Organizations structure with management account and member accounts
2. **Security Services Layer**: GuardDuty, Inspector, Macie, and CSPM icons distributed across accounts
3. **Aggregation Layer**: Security Hub (delegated administrator) with OCSF normalization engine
4. **Correlation Layer**: Exposure finding engine showing attack path analysis
5. **Integration Layer**: Bidirectional arrows to Jira/ServiceNow and SIEM platforms
6. **Data Flow**: Color-coded arrows showing threat, vulnerability, compliance, and data security findings flowing into Security Hub

## Technologies Used

- **AWS Security Hub** - Central security and compliance aggregation service providing unified finding management, OCSF normalization, and advanced correlation capabilities for exposure detection and attack path analysis
- **Amazon GuardDuty** - Intelligent threat detection service continuously monitoring AWS accounts for malicious activity, unauthorized behavior, and anomalous API calls with 30-day trial coverage
- **Amazon Inspector** - Automated vulnerability management service performing continuous scanning for software vulnerabilities and unintended network exposure with 15-day trial period
- **AWS Security Hub CSPM** - Cloud Security Posture Management service evaluating AWS resources against security best practices and compliance frameworks (CIS, PCI-DSS, NIST) with 30-day trial
- **Amazon Macie** - Sensitive data discovery and classification service using machine learning to identify and protect PII, PHI, and financial data with 30-day trial coverage
- **AWS Organizations** - Multi-account management service enabling centralized governance, service control policies, and delegated administration for security services
- **OCSF (Open Cybersecurity Schema Framework)** - Vendor-agnostic schema standardizing security event data for seamless integration with SIEM, SOAR, and analytics platforms
- **AWS Labs GuardDuty Findings Tester** - Open-source testing framework generating realistic GuardDuty findings for validation of detection and correlation pipelines
- 
## Skills Demonstrated
- **Cloud Security Architecture Design** - Architected enterprise-grade security operations platform leveraging AWS-native services with centralized management and distributed enforcement patterns
- **Multi-Account Security Governance** - Implemented AWS Organizations integration with delegated administrator configuration for scalable security management across organizational boundaries
- **Security Service Integration** - Orchestrated complex integration of five AWS security services with synchronized activation timing to optimize trial period coverage and evaluation effectiveness
- **Threat Detection and Response** - Validated end-to-end threat detection pipelines from GuardDuty finding generation through Security Hub correlation to ITSM ticket creation
- **Vulnerability Management** - Demonstrated continuous vulnerability assessment workflows combining Inspector scanning with Security Hub prioritization and exposure correlation
- **Compliance Automation** - Configured automated compliance evaluation against multiple frameworks (CIS, PCI-DSS, NIST) with centralized reporting and remediation tracking
- **Data Security and Privacy** - Implemented sensitive data discovery and classification workflows using Macie with integration into unified security operations platform
- **Security Data Normalization** - Applied OCSF framework for standardizing security telemetry enabling vendor-agnostic integration with enterprise security tools
- **Attack Surface Analysis** - Leveraged exposure finding correlation to identify network-exploitable vulnerabilities and visualize potential attack paths with blast radius assessment
- **Security Operations Optimization** - Designed workflows reducing alert fatigue through intelligent finding correlation, prioritization, and automated routing to appropriate response teams
- **Security Testing and Validation** - Executed comprehensive testing protocols using AWS Labs tools to validate detection capabilities and correlation accuracy

## Implementation Details

### Planning and Assessment Phase

The implementation began with a comprehensive planning phase to establish clear success criteria and evaluate organizational readiness. Key activities included assessing AWS Organizations permissions, inventorying existing security service deployments, and designing an activation timeline that would maximize the value of trial periods across multiple services. A critical design decision involved coordinating service activation to ensure at least two weeks of overlapping coverage between the shortest trial period (Inspector at 15 days) and longer trials (GuardDuty, Macie, and CSPM at 30 days).

**Success Criteria Defined:**
- Successful integration of all five security services with Security Hub
- Validation of finding correlation across service boundaries
- Demonstration of exposure finding generation with attack path visualization
- Functional ITSM integration with automated ticket creation
- Comprehensive evaluation of OCSF normalization capabilities

### Strategic Service Activation

Service activation followed a carefully orchestrated timeline to optimize trial period overlap and ensure comprehensive security coverage during evaluation:

```bash
# Day 1: Simultaneous activation of all services
# This ensures minimum 15-day overlap across all services

# Enable Security Hub at organization level
aws securityhub enable-organization-admin-account \
  --admin-account-id 123456789012

# Enable GuardDuty with all protection plans (30-day trial)
aws guardduty create-detector \
  --enable \
  --finding-publishing-frequency FIFTEEN_MINUTES \
  --data-sources S3Logs={Enable=true},Kubernetes={AuditLogs={Enable=true}},MalwareProtection={ScanEc2InstanceWithFindings={EbsVolumes={Enable=true}}}

# Enable Inspector v2 (15-day trial)
aws inspector2 enable \
  --resource-types EC2 ECR LAMBDA

# Enable Macie (30-day trial)
aws macie2 enable-macie

# Enable Security Hub CSPM (30-day trial)
aws securityhub update-security-hub-configuration \
  --enable-default-standards \
  --control-finding-generator SECURITY_CONTROL
```

**Trial Period Optimization Strategy:**
- **Days 1-15**: Full coverage across all services (GuardDuty, Inspector, Macie, CSPM, Security Hub)
- **Days 16-30**: Continued coverage from GuardDuty, Macie, and CSPM after Inspector trial expiration
- **Evaluation Focus**: Concentrated intensive testing during days 5-15 to maximize overlapping service coverage

### Multi-Region and Multi-Account Configuration

I implemented a delegated administrator pattern for centralized security management while maintaining account autonomy:

```bash
# Configure delegated administrator for Security Hub
aws organizations register-delegated-administrator \
  --account-id 123456789012 \
  --service-principal securityhub.amazonaws.com

# Enable Security Hub in all required regions
REGIONS=("us-east-1" "us-west-2" "eu-west-1" "ap-southeast-1")

for region in "${REGIONS[@]}"; do
  aws securityhub enable-security-hub \
    --region $region \
    --enable-default-standards \
    --control-finding-generator SECURITY_CONTROL
  
  # Enable integrations in each region
  aws securityhub batch-enable-standards \
    --region $region \
    --standards-subscription-requests \
      StandardsArn=arn:aws:securityhub:$region::standards/cis-aws-foundations-benchmark/v/1.4.0 \
      StandardsArn=arn:aws:securityhub:$region::standards/pci-dss/v/3.2.1
done
```

### Service Integration and Finding Aggregation

Security Hub was configured to receive findings from all integrated security services with appropriate filtering and aggregation rules:

### Testing and Validation Methodology

Comprehensive testing validated the end-to-end security operations workflow:

```bash
# Clone and execute GuardDuty Findings Tester
git clone https://github.com/awslabs/amazon-guardduty-tester.git
cd amazon-guardduty-tester

# Deploy test infrastructure
./guardduty-tester.sh --region us-east-1 --create

# Generate test findings (various attack scenarios)
./guardduty-tester.sh --region us-east-1 --run-all

```

**Validation Checklist:**
- ✅ GuardDuty findings appear in Security Hub within 5 minutes
- ✅ Inspector vulnerability findings correlated with network reachability data
- ✅ Exposure findings generated for internet-facing resources with critical CVEs
- ✅ Attack path visualization displays multi-hop exploitation scenarios
- ✅ OCSF-normalized findings successfully ingested by SIEM platform
- ✅ Automated tickets created in Jira with correct severity mapping
- ✅ Compliance findings aggregated across all member accounts
- ✅ Macie sensitive data findings integrated with data security dashboard
