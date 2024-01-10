# Spam Patriot

## Origins
This project is designed in ~1hr as a response to a scam that someone was sent that we (a small group of Hack Clubers) wanted to shut down.

## Overview
Basicaly how this project works is it creates a new thread every so many milliseconds (configurable) and sends a request to the specified url with random data generated with the faker library.

### Fake data generated:
With the base config straight out of this repo it will spam [https://www.hhposall.xyz/](https://www.hhposall.xyz/) with a set of random, fake data. Here's a summary of each key-value pair:
- 'murmur': A random string of 32 lowercase letters and digits.
- 'uid': A random integer between 1 and 100,000.
- 'first_name': A fake first name generated by the faker library.
- 'last_name': A fake last name generated by the faker library.
- 'phone': A fake phone number generated by the faker library.
- 'email': A fake email address generated by the faker library.
- 'address': A fake address generated by the faker library.
- 'city': A fake city name generated by the faker library.
- 'zip': A fake zip code generated by the faker library.
- 'state': A fake state abbreviation generated by the faker library.

## Configuration
To adapt this to your target you will need to modify the following:
1. The data fields; change the keys to be the keys of the targets api and the data to be the correct faker values (line 26: spam.py):
    ```python
    random_data = {
        'murmur': ''.join(random.choices(string.ascii_lowercase + string.digits, k=32)),
        'uid': str(random.randint(1, 100000)),
        'first_name': fake.first_name(),
        'last_name': fake.last_name(),
        'phone': fake.phone_number(),
        'email': fake.email(),
        'address': fake.address(),
        'city': fake.city(),
        'zip': fake.zipcode(),
        'state': fake.state_abbr()  # You can modify this according to your needs
    }
    ```
2. The correct URL (line 11: spam.py):
    ```python
    url = 'https://www.hhposall.xyz/php/app/index/verify-info.php?t='
    ```

3. Any url parameters that need to be randomized (line 42: spam.py):
    ```python
    urlwithnum =  url + str(random.randint(1000000000000, 9999999999999))
    ```

4. Set running mode; the first paramter is the spam count; second is whether to run in infinite mode (first param wouldn't matter then) or not; time between thread creation; and time between batch of 100 threads (line 122: spam.py):
    ```python
    spamRequests(10000, False, 0.05, 3)
    ```
