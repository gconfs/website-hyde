In order to setup a remote server that is going to generate and serve the
files, you have to create a bare repository:

```
# On the server
mkdir website.git
cd website.git
git --bare init
```

Then you have to copy the script that will generate the website:

```
# On the server
cp post-receive website.git/hooks/
```

Finally, on each client, you can add the remote server to the git configuration
and add your SSH key to the `authorized_keys` of the server:

```
$ # On the client
$ git remote add server git@gconfs.fr:~/website.git
$ git push server master
Décompte des objets: 3, fait.
Delta compression using up to 8 threads.
Compression des objets: 100% (3/3), fait.
Écriture des objets: 100% (3/3), 406 bytes | 0 bytes/s, fait.
Total 3 (delta 1), reused 0 (delta 0)
remote: Cloning into '/home/git/tmp/website'...
remote: done.
remote:  20:18:39 hyde.engine Reading site configuration from
[/home/git/tmp/website/site.yaml]
remote:  20:18:40 hyde.engine Reading site contents
remote:  20:18:40 hyde.engine Generating site at [/home/git/tmp/website]
remote:  20:18:40 hyde.engine Configuring the template environment
remote:  20:18:40 hyde.engine Generating site to [/home/git/build]
remote:  20:18:47 hyde Generation complete.
To git@gconfs.fr:/home/git/website.git
   5023945..d29e802  master -> master
```
