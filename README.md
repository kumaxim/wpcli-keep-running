# WP CLI: Keep Running Containers

Change CMD from ["wp", "shell"] to ["tail", "-f", "/dev/null"] in WP CLI images

Based on [Official WordPress Images](https://hub.docker.com/_/wordpress)