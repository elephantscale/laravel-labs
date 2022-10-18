# Laravel Advanced Workshop 

## Requirements

In your Manage Cars app implement the following

- Build an API with the following endpoints

  - Get all Cars
  - Get a single car by Id
  - Get all brands


- Implement Redis Cache in all methods with the following durations

  - Get all Cars (10 mins)
  - Get a single car by Id (2 hours)
  - Get all brands (12 hours)

The cache should be cleaned when a new car is added or updated


- Add rate limit to all endpoints with the following specifications

    - Get all Cars (Max 10 times per minute)
    - Get a single car by Id (Max 2 times per minute)
    - Get all brands (Max 25 times per hour)

Also all endpoints should have a custom response indicating the time to wait for the next request.


