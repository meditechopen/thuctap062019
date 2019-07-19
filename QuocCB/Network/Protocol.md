### Protocol

One of the important networking concepts is *Protocol*.

Definition: A formal description of message formats and the rules two or more machine must follow to exchange those messages.

The *Protocol* usualy exist in two forms. First, they exist in a textual form for human to understand. Second, they exist as programming code for computer to understand.
Both forms should untimately specify the precise interpretation of every bit of every message exchange across the network.

Protocols exist at every point where logical program flow crosses between hosts.
In other words, we need protocols every time we want to do something on another computer.
Every time we want to print something on a network printer we need protocols.
Every time we want to download a file we need protocols.
Every time we want to save our work on disk, we don't need protocols - unless the disk is on a network file server.  

Protocols exist at every point where logical program flow crosses between hosts.
In other words, we need protocols every time we want to do something on another computer.
Every time we want to print something on a network printer we need protocols.
Every time we want to download a file we need protocols.
Every time we want to save our work on disk, we don't need protocols - unless the disk is on a network file server.

### Protocol Layering

Protocols define the format of the messages exchanged over the Internet.
They are normally structured in layers, to simplify design and programming.

Protocol layering is a common technique to simplify networking designs by dividing them into functional layers, and assigning protocols to perform each layer's task.

For example, it is common to separate the functions of data delivery and connection management into separate layers, and therefore separate protocols.
Thus, one protocol is designed to perform data delivery, and another protocol, layered above the first, performs connection management.
The data delivery protocol is fairly simple and knows nothing of connection management.
The connection management protocol is also fairly simple, since it doesn't need to concern itself with data delivery.

Protocol layering produces simple protocols, each with a few well-defined tasks.
These protocols can then be assembled into a useful whole.
Individual protocols can also be removed or replaced as needed for particular applications.

The most important layered protocol designs are the Internet's original DoD model, and the OSI Seven Layer Model. The modern Internet represents a fusion of both models.