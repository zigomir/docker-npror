### Docker

- CMD get will be executed when you run an image [learned from](http://blog.stefanxo.com/2014/01/breaking-down-a-dockerfile/)
- if you change line in Dockerfile you'll lose all the cache, so only add new commands at the end if you 
want to preserve cache - need to test that; [source](http://crosbymichael.com/dockerfile-best-practices.html)