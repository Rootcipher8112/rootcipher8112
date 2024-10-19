# e-Commerce Risk Analysis  
**Jason Rowe**  
10/1/24  

## Project Introduction: e-Commerce Risk Analysis Scenerio

This project involves conducting a comprehensive e-commerce risk analysis for Bay & Shore General Store (BSGS), a fictional small business with three physical locations. Faced with declining sales due to reduced tourism and foot traffic, BSGS is planning to expand its operations by launching an online storefront. The fictional consulting company I work for has been tasked with assessing potential cybersecurity risks related to this expansion, ensuring that the store's move to e-commerce is both secure and financially viable.  

Drawing from real-world scenarios, this analysis leverages best practices in the industry and examines the cybersecurity measures of similar e-commerce businesses such as Amazon, Etsy, and 1-800-Flowers. The goal is to identify key risks and propose actionable strategies to protect BSGS from cyber threats, with a focus on payment security, data protection, and maintaining customer trust.


## Synopsis: Bay & Shore General Store Overview  
Bay & Shore General Store (BSGS) is a small business that operates three brick-and-mortar stores located in Annapolis, MD, Bethany Bay, DE, and Ocean City, NJ. The store features a range of products including themed clothing, gifts, home décor, and handmade confections. The Delaware and New Jersey locations also sell fresh produce and specialty food items sourced from local suppliers. BSGS's marketing emphasizes its strong ties with local communities, including partnerships with local artisans, farmers, and other producers, highlighting the positive social and economic impact its operations have on these areas (King 2021).  

In recent years, BSGS has experienced a significant downturn in sales at its physical locations due to decreased tourism and foot traffic. However, the store has seen an uptick in telephone and email sales, prompting the owner to consider expanding the business by setting up an e-commerce storefront (King 2021). This shift to an online platform requires careful risk assessment, especially in terms of cybersecurity and IT security risks, which are critical to the financial viability of the expansion.  

The company has turned to Nofsinger Consultants for assistance in assessing the cybersecurity risks and developing strategies to mitigate those risks. This risk assessment will help satisfy loan requirements for banks considering funding the expansion (King 2021). By analyzing the risks faced by similar e-commerce businesses such as 1800Flowers, Amazon, and Etsy, the assessment will draw on publicly available information, including annual reports and NIST guidelines, to propose risk controls and strategies suitable for BSGS.  

## Industry Introduction: E-Commerce and Payment Card Security  
The e-commerce industry has grown exponentially over the past two decades, revolutionizing the way businesses operate and how consumers shop. With the rise of platforms like Amazon, Etsy, and 1-800-Flowers, consumers now have global access to a variety of products at their fingertips. However, with this convenience comes significant responsibility regarding the protection of sensitive consumer information, particularly payment data.  

Central to e-commerce security is the Payment Card Industry Data Security Standard (PCI DSS), which was developed to secure payment card transactions and protect cardholder data. PCI DSS applies to any organization that processes, stores, or transmits payment card information, mandating requirements such as data encryption, strong access control measures, and regular security testing (PCI Security Standards Council 2024). For e-commerce companies, PCI DSS compliance is not just a regulatory requirement but a vital component of maintaining customer trust and ensuring secure online transactions.  

### Amazon Business Profile  
- **Headquarters Location:** Seattle, Washington, USA  
- **Key Personnel:**
  - Andy Jassy – CEO
  - Brian T. Olsavsky – CFO
  - Doug Herrington – CEO Worldwide Amazon Stores
- **Primary Business Activities:**  
Founded in 1994 by Jeff Bezos, Amazon has become the world's largest online retailer. The company operates in diverse sectors including retail, cloud computing, and entertainment. Amazon’s e-commerce platform offers products ranging from electronics to books and clothing. In addition, Amazon Web Services (AWS) provides cloud computing services that form the backbone of many online businesses and organizations globally (Amazon.com 2020).  
- **Major Products or Services Sold:**  
  - Consumer goods (electronics, apparel, books, etc.)  
  - Amazon Prime (subscription services)  
  - AWS (cloud services)  
  - Proprietary devices (e.g. Kindle, Fire TV)  
- **Recent Financial Performance:**  
Amazon reported a revenue of $386 billion in 2020, driven by the rise in online shopping during the COVID-19 pandemic (Amazon.com 2020). The company's rapid expansion into various sectors has solidified its dominance in the global market.  
- **Major Competitors:**  
  - Alibaba  
  - Walmart  
  - eBay  
- **Cybersecurity Needs:**  
Due to its vast e-commerce platform, Amazon handles sensitive customer information, including payment card details. This requires strong cybersecurity measures including data encryption, identity and access management, and robust threat detection systems. AWS also plays a critical role in Amazon’s cybersecurity framework, offering secure cloud services to both internal operations and external customers (Amazon AWS n.d.).  

### Etsy Business Profile  
- **Headquarters Location:** Brooklyn, New York, USA  
- **Key Personnel:**
  - Josh Silverman – CEO  
  - Rachel Glaser – CFO  
- **Primary Business Activities:**  
Founded in 2005, Etsy is a leading online marketplace for handmade, vintage, and unique goods. It connects millions of independent artisans and craftspeople to a global audience. Etsy’s focus on creativity and individuality allows sellers to offer products that cater to niche markets, creating a vibrant community of buyers and sellers (Etsy INC 2020).  
- **Major Products or Services Sold:**  
  - Handmade goods (jewelry, apparel, home décor)  
  - Vintage items  
  - Craft supplies  
- **Recent Financial Performance:**  
In 2020, Etsy reported $1.7 billion in revenue, benefiting from the surge in online shopping during the pandemic. The platform saw significant growth in its user base, with over 96 million active buyers and around 9 million sellers by the end of the year (Etsy INC 2020).  
- **Major Competitors:**  
  - Amazon Handmade  
  - eBay  
  - Shopify  
- **Cybersecurity Needs:**  
Etsy’s platform processes numerous small transactions daily, making secure payment processing a priority. The company complies with PCI DSS to protect customer payment information and employs additional cybersecurity measures to prevent fraud and ensure the integrity of its marketplace. Etsy’s Bug Bounty Program also encourages the identification and reporting of security vulnerabilities, further enhancing its cybersecurity infrastructure (Vigderman 2024).  

### 1-800-Flowers Business Profile  
- **Headquarters Location:** Jericho, New York, USA  
- **Key Personnel:**
  - Chris McCann – CEO  
  - Bill Shea – CFO  
- **Primary Business Activities:**  
Founded in 1976, 1-800-Flowers is a premier floral and gourmet gift retailer. The company operates multiple brands, including Harry & David, Cheryl's Cookies, and The Popcorn Factory, catering to customers seeking gifts for various occasions. The company’s e-commerce platform plays a crucial role in driving sales and delivering products nationwide (1 800 FLOWERS COM INC 10-K 2024).  
- **Major Products or Services Sold:**  
  - Floral arrangements  
  - Gourmet gift baskets  
  - Specialty foods  
- **Recent Financial Performance:**  
For the fiscal year 2023, 1-800-Flowers reported over $2.1 billion in revenue, reflecting steady growth in its e-commerce business. The company has effectively leveraged its online presence to reach a broader customer base (1 800 FLOWERS COM INC 10-K 2024).  
- **Major Competitors:**  
  - Teleflora  
  - FTD  
  - ProFlowers  
- **Cybersecurity Needs:**  
Given its reliance on online transactions, 1-800-Flowers must ensure the security of its customer data and payment information. The company’s supply chain and third-party vendors also introduce additional cybersecurity risks, requiring comprehensive security strategies that include encryption, PCI DSS compliance, and regular security assessments (Seals 2018).

## Common Risks and Their Potential Impact on Bay & Shore General Store  
| **ID** | **Use Case**                           | **Description of Risk**                                               | **Potential Impacts to BSGS (Harm or Loss)**                                                                 |
|-------|----------------------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| 1     | Customer browses an online catalog      | Risk of website defacement or data breach. Attackers could exploit vulnerabilities to deface the website or steal customer data. | BSGS could lose customers’ trust, face reputational damage, and be liable for non-compliance with data protection regulations.  |
| 2     | Customer makes a product purchase       | Payment card data theft. Cybercriminals could intercept or steal payment information during transactions.     | BSGS could experience financial losses due to fraud, suffer from regulatory fines (i.e., PCI DSS non-compliance), and damage its brand. |
| 3     | Company bills customer for items/shipping | Unauthorized access to billing systems. Attackers could gain access to sensitive billing information and steal or manipulate payment data. | BSGS could incur significant financial losses and experience system outages, disrupting business operations. |
| 4     | Employee fills order and ships to customer | Compromised employee accounts. Insider threats or social engineering attacks could lead to unauthorized order processing. | BSGS might ship incorrect or fraudulent orders, leading to customer dissatisfaction, additional costs, and operational inefficiencies. |
| 5     | Customer initiates return of a delivered product | Fraudulent return requests. Customers could exploit the return policy for fraudulent returns or product manipulation. | BSGS could face financial loss from fraudulent returns and see increased operational costs due to fake product returns. |
| 6     | Employee enters a price change for an item in inventory | Privilege escalation attack. Attackers could exploit internal systems to escalate privileges and modify product prices fraudulently. | BSGS could lose revenue by selling underpriced goods or face reputational damage if customers exploit manipulated prices. |
| 7     | Manager checks sales report             | Unauthorized access to sensitive sales data. Attackers could steal or manipulate sales reports and financial information. | BSGS could experience significant financial harm if sensitive data is leaked or manipulated, and decision-making could be compromised. |
| 8     | Manager authorizes refund               | Refund fraud. Criminals could use stolen payment card data or false claims to process unauthorized refunds.   | BSGS could face financial losses, increased operational costs, and risks to brand reputation if fraudulent refunds become common. |

## Summary of Identified Risks and Their Impacts  
1. **Data Breaches and Website Defacement:** Customers browsing the Bay & Shore General Store’s catalog are at risk if the website's security is compromised. Attackers could deface the website, damaging the brand's reputation and disrupting operations (Amazon.com 2020).  
2. **Payment Card Fraud:** During purchase transactions, BSGS faces a high risk of payment card data theft. PCI DSS standards must be strictly adhered to in order to avoid theft of payment information during online transactions, as seen in the breaches experienced by 1-800-Flowers (Seals 2018).  
3. **Billing System Compromise:** Billing systems are a critical point for cyberattacks. If an attacker gains unauthorized access, they could manipulate or steal sensitive billing data, leading to financial and reputational damage for BSGS (PCI Security Standards Council 2024).  
4. **Insider Threats:** Employees tasked with fulfilling orders could become a target for social engineering or insider threats. These risks could result in fraudulent or incorrect shipments, increasing operational costs and reducing customer satisfaction (Vigderman 2024).  
5. **Return Policy Exploitation:** Fraudulent return claims are a growing risk for e-commerce companies. BSGS could be impacted by customers exploiting return policies for personal gain, leading to revenue loss and inefficiencies (Etsy INC 2020).  
6. **Privilege Escalation Attacks:** An attacker who manages to gain elevated access within the company could change the prices of products. This could result in lost revenue or potential legal issues if customers take advantage of erroneously reduced prices (Amazon.com 2020).  
7. **Unauthorized Data Access:** Access to sales reports by unauthorized individuals poses a significant risk. Financial data, customer information, and other critical business data could be compromised, leading to business disruption and potential fines for non-compliance (National Institute of Standards and Technology 2012).  
8. **Refund Fraud:** Fraudulent refunds are a common risk in e-commerce. Criminals could exploit BSGS's refund policies using stolen payment information or by submitting false refund requests, leading to financial losses (PCI Security Standards Council 2024).

## Recommendations for Bay & Shore General Store's Cybersecurity Strategy  
### Overview of Cybersecurity Business Needs  
Bay & Shore General Store (BSGS) operates in the e-commerce space, requiring a robust cybersecurity strategy to protect its sensitive customer data, payment card information, and ensure the availability and integrity of its website. The business needs for cybersecurity revolve around protecting against common risks such as payment fraud, insider threats, denial-of-service attacks, and data breaches, which are prevalent in the e-commerce industry.  

To meet these needs, BSGS must adopt a multi-layered cybersecurity approach, ensuring that both front-end customer transactions and back-office processes are secured. The cybersecurity strategy should focus on securing payment card transactions, protecting personal identifiable information (PII), maintaining system uptime, and securing the company’s internal systems from both external and internal threats.  

### Risk Management Strategy  
An effective risk management strategy for BSGS should include the following four major risk treatments: accept, avoid, mitigate, and transfer. Each risk treatment will be applied to the identified risks from the previous section.  

#### Risk Acceptance  
Risk acceptance is applicable when the potential harm or impact of a risk is minimal and the cost of mitigation outweighs the benefits. For example, minor system outages caused by routine maintenance might not be worth the cost of implementing complex high-availability systems. In this case, BSGS could accept the risk of brief non-critical downtime as the financial or reputational impact would be minimal (National Institute of Standards and Technology 2012).  

#### Risk Avoidance  
Risk avoidance entails avoiding actions or systems that pose high risk to the organization. In BSGS's case, storing payment card information could expose the company to significant financial and reputational risks if breached. To avoid these risks, BSGS should outsource payment processing to third-party providers who comply with PCI DSS (PCI Security Standards Council 2024). By leveraging external payment processors like PayPal or Stripe, BSGS can avoid storing sensitive financial data and thus reduce the risk of data breaches related to payment information.  

#### Risk Mitigation  
Risk mitigation involves implementing controls and countermeasures to reduce the likelihood or impact of a risk. Most of BSGS's risks, such as data breaches, fraudulent transactions, and insider threats, can be mitigated through a variety of security controls. These measures include:  
- **Encryption:** Encrypting all sensitive data, including customer PII and payment information both in transit and at rest using AES-256 encryption ensures data protection against breaches and unauthorized access (Agarwal n.d.).  
- **Multi-Factor Authentication (MFA):** Implementing MFA for all employee access to critical systems and customer accounts reduces the risk of unauthorized access via compromised credentials (Amazon AWS n.d.).  
- **Regular Security Audits:** Conducting periodic security audits and vulnerability scans to identify weaknesses in the system. For example, scanning for SQL injection vulnerabilities or testing for cross-site scripting (XSS) risks ensures the website remains secure (Etsy INC 2020).  
- **Security Awareness Training:** Regularly training employees on security best practices, including identifying phishing attempts and following secure processes, will reduce insider threats and accidental breaches (Vigderman 2024).  

#### Risk Transfer  
Risk transfer involves shifting the financial impact of risks to a third party. BSGS can transfer some of its risks by investing in cyber insurance policies. These policies would help cover the costs associated with data breaches, including legal fees, customer notifications, and remediation efforts (Tyas Tunggal 2024). Additionally, outsourcing key functions like cloud hosting and payment processing can transfer some cybersecurity risks to third-party providers who specialize in those areas and assume the responsibility for ensuring security compliance.  

### Recommendation Against Risk Treatments Not to Use  
While the four risk treatments cover a comprehensive range of strategies, risk avoidance is not suitable for every scenario. For instance, avoiding the use of e-commerce or online payment systems entirely would eliminate risks but would also prevent BSGS from participating in a critical market. Therefore, while avoidance may be appropriate in specific high-risk areas (such as avoiding storing payment card data), it is not advisable for most business operations that are essential for growth and competitiveness in the digital marketplace.  

## Recap  
Bay & Shore General Store’s cybersecurity needs focus on protecting sensitive customer information, maintaining the integrity of e-commerce transactions, and ensuring operational resilience. A multi-layered cybersecurity strategy that applies the four risk treatments—accept, avoid, mitigate, and transfer—can effectively address the most pressing risks. By implementing strong encryption, utilizing third-party payment processors, conducting regular security audits, and transferring some risks to insurance providers, BSGS can create a secure and resilient e-commerce operation. These steps will help safeguard the company against common threats in the e-commerce industry and ensure the protection of both its customers and business operations.  

## References  
- 1 800 FLOWERS COM INC 10-K Cybersecurity GRC - 2024-09-06. (2024, September 6). Board Cybersecurity. https://www.board-cybersecurity.com/annual-reports/tracker/20240906-1-800-flowers-com-inc-cybersecurity-10k/  
- 1800 Flowers. (2021, September 10). 1 800 FLOWERS COM INC Annual report. Investis.com. Retrieved September 12, 2024, from https://otp.tools.investis.com/clients/us/1-800-flowers1/SEC/sec-show.aspx?Type=html&FilingId=15219013&Cik=0001084869  
- Agarwal, R. (n.d.). Amazon Web Services Data Security: Key aspects and significance. Mgt-commerce. Retrieved September 12, 2024, from https://www.mgt-commerce.com/blog/amazon-web-services-data-security/  
- Amazon AWS. (n.d.). Cloud Security – Amazon Web Services (AWS). Amazon Web Services Inc. Retrieved September 12, 2024, from https://aws.amazon.com/security/  
- Amazon.com. (2020). 2020 Annual Report. Retrieved September 12, 2024, from https://s2.q4cdn.com/299287126/files/doc_financials/2021/ar/Amazon-2020-Annual-Report.pdf  
- Etsy INC. (2020). Etsy FORM 10-K. Retrieved September 12, 2024, from https://d18rn0p25nwr6d.cloudfront.net/CIK-0001370637/4e43d306-4e72-462c-8f1a-bcb19b770718.pdf  
- King, V. J., deGrazia, B., & University of Maryland Global Campus. (2021). Identifying & managing cybersecurity risk. https://leocontent.umgc.edu/content/dam/course-content/tus/csia/csia-350/document/Identifying%20and%20Managing%20Cybersecurity%20Risk%20-%20a%20case%20study%20for%20CSIA%20350%2830Nov2021%29.pdf?ou=1276918  
- National Institute of Standards and Technology. (2012). Guide for conducting risk assessments. In NIST Special Publication 800-30 (p. 95 pages). https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-30r1.pdf  
- PCI Security Standards Council. (2024, April). Guide to Safe Payments. pcisecuritystandards.org. Retrieved September 12, 2024, from https://www.pcisecuritystandards.org/wp-content/uploads/2022/05/Small_Merchant_Guide_to_Safe_Payments.pdf  
- Seals, T. (2018, December 4). 1800 Flowers becomes latest payment breach victim. Threat Post. https://threatpost.com/1-800-flowers-becomes-latest-payment-breach-victim/139619/  
- Tyas Tunggal, A. (2024, September 9). How does Amazon handle cybersecurity? | UpGuard. Upguard. Retrieved September 12, 2024, from https://www.upguard.com/blog/prime-day-how-amazon-handles-cybersecurity  
- Vigderman, A. (2024, July 10). Is Etsy safe? Security.org. https://www.security.org/digital-safety/is-etsy-safe/  
