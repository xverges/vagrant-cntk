# vagrant-cntk
Vagrantfile with Microsoft's [CNTK](https://docs.microsoft.com/en-us/cognitive-toolkit/)
with [Miniconda](https://conda.io/miniconda.html) and Python 3.6.1 on 
[Ubuntu 16.04](https://app.vagrantup.com/ubuntu/boxes/xenial64)
so I can use the toolkit on OSX and follow [edX - Microsoft: DEV288x Natural Language 
Processing](https://www.edx.org/course/natural-language-processing-nlp-microsoft-dev288x).

To launch Jupyter notebooks so that they can be accessed from the host,

```
vagrant@ubuntu-xenial:~$ jupyter notebook --ip=0.0.0.0
```


