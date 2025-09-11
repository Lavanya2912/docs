---
title: "Grouping-operations-with-tags.md"
pageId: "68c1a8a00a41c4013a7696ea"
---

## title: Organize API Endpoints with OpenAPI Tags authors: phil image: images/guides/tags\-organize\-endpoints.png excerpt: Learn tips and tricks to group related endpoints in a meaningful way. date: 2024\-08\-08

- TOC \{:toc\}

Tags are a great way to organize the API endpoints in your OpenAPI documents.

Typically, OpenAPI tags are used to group related endpoints in a meaningful way, such as by business function or logical objects. When using tags, you define an array of tags at the root of your document, like this:

```yaml
tags:
  - name: Stations
    description: | 
      Find and filter train stations across Europe, including their location
      and local timezone.
    externalDocs:
      description: Read more
      url: http://docs.example.com/guides/stations
  - name: Trips
    description: | 
      Timetables and routes for train trips between stations, including pricing
      and availability.
  - name: Bookings
    description: | 
      Create and manage bookings for train trips, including passenger details
      and optional extras.
  - name: Payments
    description: |
      Pay for bookings using a card or bank account, and view payment
      status and history.

      > warn
      > Bookings usually expire within 1 hour so you'll need to make your payment
      > before the expiry date 
```

Once you've created these tags, you can use them to group related endpoints in your API using the `tags` property on the endpoint as follows:

```yaml
paths:
  /stations:
    get:
      summary: Get a list of train stations
      tags:
        - Stations
  /trips:
    get:
      summary: Get available train trips
      tags:
        - Trips
```

You can also apply multiple tags to an operation:

```yaml
paths:
  /bookings/{bookingId}/payment:
    post:
      summary: Pay for a Booking
      tags:
        - Bookings
        - Payments
```

## Benefits of OpenAPI Tags

Tags are a powerful tool for improving the usability of your OpenAPI document. Below are some of the ways using tags can help keep your OpenAPI document organized.

### Tags Can Describe Endpoint Groups

When specifying your tags in the root level of your API contract, you can give context to the tag using the `description` property. Let’s take [Bump.sh API documentation](https://bump.sh/demo/doc/bump). Here is how the `Diffs` tag is created and described in [Bump.sh API Contract](https://developers.bump.sh):

```yaml
tags:
  - name: Diffs
    description: Diff summary of changes in the API
```

The documentation will show the `Diffs` property like this: