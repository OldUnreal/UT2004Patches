# Unreal Engine Network Compatibility Notes

This is a non-exhaustive list of things you can and cannot do if you want to
make changes to the UnrealScript code whilst preserving network compatibility
with older versions of the game.

## 1. Adding new variables to an existing UnrealScript class

:white_check_mark: This is fine in most cases.

:question: One potential issue, however, is that the same variable might be
declared (and marked as replicated) in a 3rd party subclass. We have yet to
check what the consequences would be.

## 2. Removing variables/functions/states from an existing UnrealScript class

:x: There are several reasons why this is not ok. First, 3rd party subclasses
might refer to or even import the removed variable/function/state. These
subclasses will no longer load.

Second, if the removed variable/function/state was marked as replicated, older
peers will still assume that they can safely replicate changes to the variable's
value or safely call the old function/state, while this is absolutely unsafe.

## 3. Marking existing non-replicated variables/functions as replicated

:x: This is a big no-no! We found out the hard way. If you mark an _existing_
variable/function as replicated, the peer that has the updated definition of the
variable/function will assume that the variable was also replicated in older
game versions. This makes the newer peer incorrectly build the class cache for
the class that contains the variable/function. In the worst case, for variables,
it can also cause peers to disagree on the maximum number of bits they need to
reserve for replication indices when replicating an object of the class that
contains the variable.

## 4. Adding new functions to an existing UnrealScript class

:white_check_mark: This is fine in most cases.

:question: One potential issue, however, is that the same variable might be
declared (and marked as replicated) in a 3rd party subclass. We have yet to
check what the consequences would be.

:exclamation: A potential compatibility problem can occur when a subclass
overrides the new function. When you compile a function that exists in a
superclass, UCC will automatically generate an import of the super function. In
this particular case, the import would refer to a function that did not exist in
older game versions. The package containing the subclass would, therefore, fail to
load in older game versions.

OldUnreal's version of UCC automatically detects this compatibility problem and
can optionally fix the import so it refers to a superfunction that _does_ exist
in older game versions.

## 5. Modifying existing functions/states in an existing UnrealScript class

:white_check_mark: This is fine in principle.

:exclamation: One thing to keep in mind, however, is that subclasses might
override the function/state and not call the super function/state. Thus, if you
want to fix a bug by modifying an existing function/state, you should absolutely
try to minimize the scope of that fix. Ideally, every fix should modify only one
function/state.

In some cases, however, you might have to modify several functions/states to
apply a fix. If that is the case, you should always keep in mind that subclasses
might completely override one (or several) of the functions/states you
modified. Thus, you should try to ensure that the basic functionality of the
class remains intact even when a subclass discards a part of your fix.

## 6. Adding new states to an existing UnrealScript class

:white_check_mark: This is usually fine for non-actor objects.

:x: You should, however, never add new states to an actor object because doing
so might result in two peers disagreeing on which state an actor object is
in. This can cause a lot of network compatibility problems.

## 7. Adding function parameters to an existing function within an existing UnrealScript class

:x: This is not ok. If you call a function, locally or remotely, the engine will
evaluate _all_ parameters and write the results of the evaluation in the
callee's stack frame just prior to jumping to the callee. If you add new
parameters to an existing function, but then call an old variant of the function
(remotely or in a subclass that was compiled against the old version), the
evaluation of the new parameters will likely cause the game to write outside the
bounds of the callee's stack frame. This can cause memory corruption and
stability problems.

## 8. Removing function parameters from an existing function within an existing UnrealScript class

:x: The engine can deal with this in principle. All parameters you pass to a
function will be evaluated and the results of the evaluation will be written to
the callee's stack frame. If you remove a parameters, the stack space reserved
for the results of that parameter's evaluation, will just remain zeroed out.

However, if the caller is a remote peer or a 3rd party package that does not
know the new definition, it will pass too many parameters to the
function. Evaluating the excess parameters can cause stack corruption, as
explained above.

## 9. Adding new UnrealScript classes

:white_check_mark: This is fine for non-networked objects (i.e., non-actor
objects or actor objects that are only spawned in a local level).

:exclamation: We discourage adding new actor objects, however. In principle, it
is possible to add new actor objects, and even to spawn them in the level. The
actor simply won't be replicated to older peers. There are many cases, however,
where not replicating certain actors causes game glitches or a heavily degraded
playing experience.

## 10. Removing existing UnrealScript classes

:x: This is not ok. 3rd party packages might refer or import the class. Removing
the class will break these 3rd party packages.
