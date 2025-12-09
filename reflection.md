# Reflection:

**Which parts of the design you feel most confident about, and which parts you are least sure about.**

I feel the most confident about the overall workflow and architecture design. The web-based intake form, cloud storage for images, and structured database for triage and patient information all make sense and are realistic. Using serverless compute with Cloud Run and Cloud Functions for the triage logic and background processes feels flexible and cost-efficient for a small prototype.

I’m less confident about the analytics and predictive parts. The architecture works well for basic reporting and lightweight analysis, but I’m not sure how it would handle more complex decision-support models or larger patient volumes.

**At least one alternative architecture you considered and why you did not choose it.**

One alternative architecture I considered was 

**If you had 4–8 more weeks and unlimited credits, what next steps you would implement.**

If I had more time and unlimited credits, I would focus on adding predictive analytics, like patient risk scoring and real-time notification systems for the staff. I would like to add AI models to create a more intelligent symptom analyzer. These models will always need human oversight, especially when AI or codes are used to make decisions on patients. I think I would also plan on integrating FHIR APIs to exchange data with EHR systems since healthcare has a lot of problems with interoperability. I would also do more research to implement more security to ensure the data is safe and secured.
