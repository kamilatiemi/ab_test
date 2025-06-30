# A/B Test Project

You have received an analytical task from an international online store. Your predecessor was unable to complete it: they launched an A/B test and then gave up (to start a watermelon farm in Brazil). They left only the technical specifications and the test results.

## Technical Description

- **Test name:** `recommender_system_test`
- **Groups:** A (control), B (new payment funnel)
- **Start date:** 2020-12-07
- **Date when they stopped receiving new users:** 2020-12-21
- **End date:** 2021-01-01
- **Audience:** 15% of new users from the EU region
- **Purpose of the test:** testing changes related to the introduction of an improved recommendation system
- **Expected result:** within 14 days after registration, users show better conversion in:
  - product page views (`product_page` event)
  - adding items to cart (`product_cart`)
  - purchases (`purchase`)

  At each stage of the funnel `product_page → product_cart → purchase`, there will be at least a 10% increase.

- **Expected number of test participants:** 6000

## Task

Download the test data, check if it was conducted correctly, and analyze the results.
