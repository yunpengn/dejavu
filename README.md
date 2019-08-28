# Dejavu

This is a audio fingerprint & recognition library implemented in Python, based on https://github.com/worldveil/dejavu with many improvements.

## Fingerprinting

Start by creating a Dejavu object with your configurations settings (Dejavu takes an ordinary Python dictionary for the settings).

```python
>>> from dejavu import Dejavu
>>> config = {
...     "database": {
...         "host": "127.0.0.1",
...         "user": "root",
...         "passwd": <password above>, 
...         "db": <name of the database you created above>,
...     }
... }
>>> djv = Dejavu(config)
```

Next, give the `fingerprint_directory` method three arguments:
* input directory to look for audio files
* audio extensions to look for in the input directory
* number of processes (optional)

```python
>>> djv.fingerprint_directory("data/audios", [".mp3"], 3)
```

For a large amount of files, this will take a while. However, Dejavu is robust enough you can kill and restart without affecting progress: Dejavu remembers which songs it fingerprinted and converted and which it didn't, and so won't repeat itself. 

You'll have a lot of fingerprints once it completes a large folder of mp3s:
```python
>>> print djv.db.get_num_fingerprints()
5442376
```

Also, any subsequent calls to `fingerprint_file` or `fingerprint_directory` will fingerprint and add those songs to the database as well. It's meant to simulate a system where as new songs are released, they are fingerprinted and added to the database seemlessly without stopping the system. 


## Licence

[MIT Licence](LICENSE)
