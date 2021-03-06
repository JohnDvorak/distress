# DISTRESS: DISTRibutEd Secure file System #

For our graduate project in Secure Data Management at the Rochester Institute
of Technology, we proposed a possible design for a secure collaborative 
file storage system. Our system uses strict client side encryption and a 
receipt based authentication system. This lets DISTRESS lend itself to a 
diverse range of applications built on top of it, such as: an anonymous 
dead-drop tool like the New Yorker's StrongBox or a friend-to-friend backup
service like CrashPlan.

## Requirements ##

Right now we have a limited set of requirements on purpose:

* Erlang VM (version R15B01 or higher)
* GNUMake or CMake

However DISTRESS is headless and will need a client to connect with it. We have
a python and C++ based client on the way. 


## Building ##

Just run `make` as long as Erlang is on the path it should work. To run DISTRESS
without having to build a release, type the following:

* `./bin/runerl.sh`
* Then once the Erlang shell starts: `distress:start().`

This is helpful for debugging the distress system before building the release.


## Installing ##

Deploying DISTRESS is simple. Running `make release` will generate a `rel` 
directory which will contain everything you need to run DISTRESS, including a
stripped down version of the Erlang VM. You can now zip/tar it up to distribute,
however just linking to the binary should be enough to run on the current 
platform:

```
make release
ln -s $(pwd)/rel/distress/bin/distress ~/bin/distress
```

Running the release is similar to a standard init.d service (with some added
features:

```
~/bin/distress
Usage: distress {start|stop|restart|reboot|ping|console|attach}
```

Once started you can `attach` to the running service and treat it like an
Erlang shell to send commands to it.

