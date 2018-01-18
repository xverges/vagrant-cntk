# vagrant-cntk
Vagrantfile with Microsoft's [CNTK](https://docs.microsoft.com/en-us/cognitive-toolkit/)
with [Miniconda](https://conda.io/miniconda.html) and Python 3.6.1 on 
[Ubuntu 16.04](https://app.vagrantup.com/ubuntu/boxes/xenial64)
so I can use the toolkit on OSX and follow [edX - Microsoft: DEV288x Natural Language 
Processing](https://www.edx.org/course/natural-language-processing-nlp-microsoft-dev288x).

Samples and tutorials are not installed. If you want to do it, ssh into the
vagrant virtual machine running `vagrant ssh` and run:

```
vagrant@ubuntu-xenial:~$ python -m cntk.sample_installer
```

To launch Jupyter notebooks so that they can be accessed from the host,

```
vagrant@ubuntu-xenial:~$ jupyter notebook --ip=0.0.0.0
```


Once you load a notebook following the instructions in the output of the previous command,
you can run any of its cells by pressing Crtl+Enter.


