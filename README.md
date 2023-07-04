# voting-app

A simple distributed application running across multiple Docker containers.

The voting app will be running at http://localhost:5000, and the results will be at http://localhost:5001.


Architecture Diagram:

![architecture excalidraw](https://github.com/SyedYakhub/voting-app/assets/87276324/f387c7a9-02a0-4cee-a972-c366ba759b36)


A front-end web app in Python which lets you vote between two options
A Redis which collects new votes
A .NET worker which consumes votes and stores them in…
A Postgres database backed by a Docker volume
A Node.js web app which shows the results of the voting in real time

Notes
The voting application only accepts one vote per client browser. It does not register additional votes if a vote has already been submitted by a client.

This isn't an example of a properly architected perfectly designed distributed app... it's just a simple example of the various types of pieces and languages you might see (queues, persistent data, etc), and how to deal with them in Docker at a basic level.
