PythonGang Chat Server and Client v1.0 Requirements Document
============================================================

*Stakeholders:* The PythonGang developer group (Developers), Eric Evans (Project Manager)

Document Modification History
-----------------------------
======== ============= ===================== ==================================
Version  Date          Author                Description
======== ============= ===================== ==================================
1.0      Aug 7th, 2017 Eric Evans            Rewrite of lost first draft
======== ============= ===================== ==================================

Project Description
-------------------
PythonGang is a group of Python programmers of varying levels of experience who have come together to build further experience and become better Python programmers.  For our first project it was decided we should build a chat server and the associated chat client to connect to that server.  This requirements document describes the requirements for creation of the first initial version of both that Chat Server and the associated Chat Client.  The project as a whole will continue on after this version is completed but the details for future versions are complex and so will not be addressed in this document.

Addressed Need
--------------
PythonGang and our Chat Server and Client have to start somewhere.  Creating a limited chat server and a simple client to go along with it will give all of our developers a chance to work together on a simple project as we learn how to develop a product as we would in a professional business.

Chat Server & Client v1.0 Purpose & Scope
-----------------------------------------
This initial version of the Chat Server & Client are not designed to be anything more than minimally functional.  The purpose of building such a rudimentary version of the software is to get all developers on the same page about how we expect development work in this group to be done.  During the creation of this version we will collectively help everyone involved learn to use Python 3.5+, Sphinx, pytest, git, and to write usable, easily understood code.

The server will continuously wait for incoming connections.  When an incoming connection is detected the server will wait for a handshake message from the client which will contain at least the user name of the user using the client.  The server will associate the user name with the connection and store that information for later use.  The server will then send a packet to all other connected clients to inform them that the new user has joined the chat room.  From that point forward messages from the client will trigger one of 3 functions in the server: 1) The default action will be to forward the data contained in the packet from the client to all other clients along with the user name associated with the sending client.  2) A client can trigger a disconnect.  If the server receives a disconnect packet it will terminate the connection to that client.  3) A client can request a list of connected users.  Upon receiving a user list request the server will send a list of all connected user names to the client that made the request.

The client will begin by asking the user for their name and the address of the chat server to connect to.  It will then connect to the server over TCP/IP.  The user will then have the capability to type text that will be sent to all other users in the chat room.  There will be some way for a user to request an updated list of all users in the chat room.  When a user closes a client it will send a disconnect message to the server to inform it they are disconnecting.

All other features should be put off until a later version of the chat server and/or client.

Timeline
--------

===================== =========================================================
Date of Completion    Milestone
===================== =========================================================
September 1st, 2017   Package leads will have created, discussed, and published
                      their initial plan for the creation of their package.
--------------------- ---------------------------------------------------------
September 15th, 2017  The test packages for each of the primary packages will
                      be completed.
--------------------- ---------------------------------------------------------
October 1st, 2017     The alpha release of each package will be completed and
                      will pass all associated tests.  At this point the server
                      and client will be available for all users within the
                      PythonGang to test and we will begin keeping a bug log.
                      This alpha release will be v0.1a.
--------------------- ---------------------------------------------------------
November 1st, 2017    All bugs we plan on fixing in this version will be
                      resolved and version 1.0 will be released.
===================== =========================================================

Functional Requirements
-----------------------

#. Users will be able to connect across the Internet to the chat server using a client.

#. The user name entered by each user into their client will be sent to and stored by the server associated with their client's connection.

#. Once successfully connected a user will be able to issue a command to the server to request a list of currently connected users.

#. While connected, any non-command sent by a user will be forwarded to all other users along with the sender's user name.

#. Also while connected, a user will be able to issue a command to the server to trigger disconnection of their own client.

#. Upon failure or disconnect of a connection the server will clean up all resources used by that connection and remove the user from the list of connected users.

#. Server will be bulletproof enough that no matter what a client sends to it the server will continue to function for all other clients.

Technical Requirements
----------------------

#. Every function or method will have at least one associated test to ensure it does what we think it should.

#. Every time a bug is found a new test will be created that triggers that bug and that test will be added to the associated test package.  This will ensure that once we have fixed the bug it will stay fixed.

#. Every function or method will have a docstring designed to be used by Sphinx's autodoc module as specified in the Sphinx doc's Python-Signatures_ section.  

#. Each function or method's docstring will include all parameters, return values, and exceptions that function may throw as is specified in the Sphinx doc's Info-Field-Lists_ section.

#. Every class will have a docstring designed to be used by Sphinx's autodoc module as specified using the Sphinx doc's Class-directive_.

#. Every module will have a docstring designed to be used by Sphinx's autodoc module as specified using the Sphinx doc's Module-directive_.

#. The server will have a command line option to allow specification of the TCP port to listen on.

.. _Python-Signatures: http://www.sphinx-doc.org/en/stable/domains.html#python-signatures

.. _Info-Field-Lists: http://www.sphinx-doc.org/en/stable/domains.html#info-field-lists

.. _Class-directive: http://www.sphinx-doc.org/en/stable/domains.html#directive-py:class

.. _Module-directive: http://www.sphinx-doc.org/en/stable/domains.html#directive-py:module


Project Constraints
-------------------

While the project has flexible time constraints we would like to keep people interested.  The milestone dates listed above should be considered the latest possible dates for those milestones but should be moved closer when ever possible.

The project's scope will not be expanded beyond the minimal system described in this document except with the permission of all package leads, and the project manager.  This version is not intended to be feature-rich.  This version is designed to be simple enough that anyone can help write it and anyone can read and understand it.  Features will be added in future versions which will have their own requirements documents.

Basic Overview Plan of Action
-----------------------------

Initially, development of the server will be separated from the development of the client.  Each will have a package lead assigned to administer it and the work will proceed similarly.  The project lead will rough out their idea of how their package (either client or server) should be built which will include what classes will be needed, how they will interact with each other within the package as a whole, what protocols will be used for communication between the client and server, and other such information.  They will write this rough design idea up in a file which will be distributed to all programmers involved in their package as well as to the Project Manager.  After some discussion, when the programmers, the package leads, and the project manager all agree that the rough design is good enough, the work breakdown structure will be updated with details about each step of development and the package lead will assign all classes, functions, etc. to one or more developers (including themselves) and coding will begin.  

The first stage of that coding will be the creation of a separate package with pytest unit test functions to test every function, class, and method in the primary package individually as well as pytest functional tests that will test to ensure that those components interact with each other as expected.  Any code that can not be tested with pytest will be brought to the attention of both package leads and the project manager and they will decide if a pytest can be skipped for that one piece of code.  Professional programming designed to create relatively bulletproof software must be test driven.  What that means is that all tests will be written before any code for the project is written.  If it is decided as development continues that the rough design for the package will need to change then the tests will be immediately updated before the design changes are made.  At any point in the development of this project we will be able to run pytest and have an in depth description of exactly what parts of our total project are functional at that given moment.  Working this way ensures 2 things:  1) Our code will function the way we expect it to both when given valid input and will fail as we expect it to when given invalid input. 2) As we write new code we can be sure we have not broken any previously working code.

For work on the primary packages (not testing packages) all packages will be stored in their own repository with their associated test package and doc package.  Each repository will have: 1) A README.rst file which will give an overview and quick start guide for using the primary package, building it's docs, and running its test package, 2) A LICENSE file containing the license that the package is distributed under (currently the plan is to put out this version under the MIT license), and 3) A /src directory which will contain subdirectories for source code for: A) the package itself (/src/<package_name>), B) the source for generating the package's full documentation (/src/doc_<package_name>), and C) the source for the test package (/src/test_<package_name>). All three directories under /src/ are packages and will include at the least a Pipfile, an __init__.py file, and any modules that are part of the package.

  
