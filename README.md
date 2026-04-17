Q5.1

Checkout is used to switch between branches. This involves updating the .pes/HEAD file to point to the selected branch, then reading the commit hash from that branch. The corresponding tree is loaded and the working directory is updated to match it. The index is also updated accordingly.

The main difficulty is handling existing changes in the working directory, since files may get overwritten if not managed properly.

Q5.2

To detect a dirty working directory, the current files are compared with the index entries. If metadata such as size or modification time differs, the file’s hash is recomputed and checked against the index.

If a difference is found and the same file also differs in the target branch, it leads to a conflict, and the checkout operation should be stopped.

Q5.3

A detached HEAD means that HEAD points directly to a commit instead of a branch.

Any new commits created in this state are not associated with a branch, so they are not referenced and can be lost. These commits can still be recovered by creating a branch using the commit hash.

Q6.1

Garbage collection starts by identifying all reachable objects from the branch heads. This includes commits, trees, and blobs, which are traversed and marked.

After that, objects in .pes/objects/ that are not marked as reachable can be deleted. A hash set can be used to efficiently store and check reachable objects.

Q6.2

Running garbage collection during a commit can cause issues. For example, objects created during a commit may not yet be referenced, and GC could mistakenly delete them.

This can result in broken commits. To prevent this, mechanisms like locking or delayed deletion are generally used.
