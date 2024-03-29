# Weather Proxy API

Web api which provides a current weather information 
from other weather services using specified format:

### Request
`GET: /weather/current/`

`curl -i -H 'Accept: application/json' http://<your server ip>/weather/current/`

### Response

```
HTTP/1.0 200 OK
Content-Type: application/json
Content-Length: 175
Server: Werkzeug/0.15.6 Python/3.7.4
Date: Fri, 13 Sep 2019 16:52:37 GMT
```

```json
{
  "humidity": {
    "percent": 100
  },
  "location": {
    "lat": 55.03,
    "lon": 82.92
  },
  "pressure": {
    "atm": 764
  },
  "temperature": {
    "C": 2.0
  },
  "timestamp": "2019-09-13T14:45:44+07:00",
  "title": "Novosibirsk"
}
```

## Getting Started

These instructions will get you a copy of the project up and 
running on your local machine for development and testing purposes.

All commands have been tested on **CentOS Linux release 7.5.1804**

### Prerequisites

Install docker and git

```bash
yum -y install git
yum -y install docker
systemctl start docker
```

### Installing

Clone the repo

```bash
git clone https://github.com/aatrubilin/wpapi
```

Go to project path

```bash
cd wpapi
```

Give the file `runme.sh` execute permission

```bash
chmod +x runme.sh
```

### Set up service

Build `Dockerfile` and run service

```bash
./runme.sh
```

Select weather api, by default service use OpenWeatherMapAPI

`Select weather api [OpenWeatherMapAPI, FakeWeatherAPI] (default OpenWeatherMapAPI): OpenWeatherMapAPI`

Set api token. Some service don't need token. For OpenWeatherMapAPI token requested.
For more information go to [https://openweathermap.org/appid](https://openweathermap.org/appid)

_Note: input coming from a terminal do not be displayed on the screen on this step_

`Weather api token: `

Set latitude and longitude. Default location is 55.03, 82.92 (Novosibirsk)

```text
City geo location, latitude [-90, 90] (default 55.03):
City geo location, longitude [-180, 180] (default 82.92):
```

Set minimum seconds between requests to service API.

`Minimum seconds between requests to API (default 60):`

After success building Dockerfile you will see 

```text
Success buid OpenWeatherMapAPI, with latitude=55.03, longitude=82.92, timeout=60
You can start api with command: docker run -p 80:5000/tcp wpapi
API is available in http://<your server ip>/weather/current/
Run service now? y/n? (default y)
```

You can run service now or later with command `docker run -p 80:5000/tcp wpapi`

To see current weather go to `http://<your server ip>/weather/current/`

## Running the tests

Install **python 3.6** or later and all requirements

```bash
yum install -y https://centos7.iuscommunity.org/ius-release.rpm
yum update -y
yum install -y python36u python36u-libs python36u-devel python36u-pip
pip3.6 install pytest
pip3.6 install -r requirements.txt
```

Set default search path for module files

```bash
export PYTHONPATH=wpapi
```

Set Openweather API key. 
For more information go to [https://openweathermap.org/appid](https://openweathermap.org/appid)

```bash
export WEATHER_API_TOKEN=<API TOKEN>
```

Run tests
```bash
python3.6 -m pytest tests/
```

## Authors

* **A.A.Trubilin** - [AATrubilin](https://github.com/AATrubilin)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

