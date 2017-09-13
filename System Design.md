### AKKA 

Akka is used for parallel and concurrency. One important feature of it is actor-model

Pros of actor model:
- Event-driven model Communication between Actors is asynchronous, allowing Actors to send messages and continue their own work without blocking.
- Strong isolation principles. They don't expose any API you can invoke. The only way you can use is sending message to ask its state
- Location transparency Actor instances can start, stop, move, and restart to scale up and down as well as recover from unexpected failures.
- Lightweight — Each instance consumes only a few hundred bytes, which realistically allows millions of concurrent Actors to exist in a single application
