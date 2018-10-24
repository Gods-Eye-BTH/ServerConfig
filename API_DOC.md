# API Documentation

This API Documentation is for the agreed upon JSON data object.
That means that this documentation will apply to the JSON dummy API,
the final API from Object Detection and it is implemented according to
this specification in both the applications and the web interface.

# Table Of Content
* /robots
* /robot
* /robot/:id
* /barriers
* JSON Examples
    * /robots
    * /robot/3
    * /barriers

# /robots
The API route `/robots` returns a JSON list of Robot objects.

# /robot/:id
The API route `/robot/:id` takes an id to show the specific robot. For example
if you wish to see the robot with id 3 your route would be `/robot/3`.

# /barriers
The API route `/barriers` returns a JSON list of Barrier Objects.

# JSON Examples
This is the JSON objects with example data. This is how the final implementation
of the API should look like from Object Detection.
## /robots

```json
[
  {
    "id": 0,
    "name": "Curiosity",
    "x": 1,
    "y": 2,
    "width": 8,
    "height": 7
  },
  {
    "id": 1,
    "name": "Tess",
    "x": 3,
    "y": 4,
    "width": 10,
    "height": 15
  },
  {
    "id": 2,
    "name": "Oportunity",
    "x": 9,
    "y": 5,
    "width": 13,
    "height": 9
  },
  {
    "id": 3,
    "name": "Mars III",
    "x": 22,
    "y": 18,
    "width": 6,
    "height": 12
  },
  {
    "id": 4,
    "name": "Beagle 2",
    "x": 32,
    "y": 45,
    "width": 10,
    "height": 15
  }
]
```

## /robot/3

```json
{
  "id": 3,
  "name": "Mars III",
  "x": 22,
  "y": 18,
  "width": 6,
  "height": 12
}
```

## /barriers

```json
[
  {
    "id": 0,
    "x": 16,
    "y": 34,
    "width": 5,
    "height": 8
  },
  {
    "id": 1,
    "x": 12,
    "y": 34,
    "width": 22,
    "height": 15
  },
  {
    "id": 2,
    "x": 34,
    "y": 22,
    "width": 12,
    "height": 13
  },
  {
    "id": 3,
    "x": 26,
    "y": 12,
    "width": 14,
    "height": 17
  }
]
```
