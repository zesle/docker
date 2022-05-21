If you're stuck in that situation, here’s my goto debugging commands to help you get a bit more information on what’s up:

### docker logs <container_id>
Hopefully you’ve already tried this, but if not, start here. This’ll give you the full STDOUT and STDERR from the command that was run initially in your container.

### docker stats <container_id>
If you just need to keep an eye on the metrics of your container to work out what’s gone wrong, docker stats can help: it’ll give you a live stream of resource usage, so you can see just how much memory you’ve leaked so far.

### docker cp <container_id>:/path/to/useful/file /local-path
Often just getting hold of more log files is enough to sort you out. If you already know what you want, docker cp has your back: copy any file from any container back out onto your local machine, so you can examine it in depth (especially useful analysing heap dumps).

### docker exec -it <container_id> /bin/bash
Next up, if you can run the container (if it’s crashed, you can restart it with docker start <container_id>), shell in directly and start digging around for further details by hand.

### docker commit <container_id> my-broken-container && docker run -it my-broken-container /bin/bash
Can't start your container at all? If you’ve got a initial command or entrypoint that immediately crashes, Docker will immediately shut it back down for you. This can make your container unstartable, so you can’t shell in any more, which really gets in the way.
Fortunately, there’s a workaround: save the current state of the shut-down container as a new image, and start that with a different command to avoid your existing failures.
Have a failing entrypoint instead? There’s an entrypoint override command-line flag too.

Read more 
https://medium.com/@pimterry/5-ways-to-debug-an-exploding-docker-container-4f729e2c0aa8
