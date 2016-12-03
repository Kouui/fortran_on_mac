# fortran_on_mac
fortran for mac and python.

## to compile:

	$ gfortran -o hello.exe helloprogram.f95
	
## to run:

	$ ./hello.exe
	
	
## simple wrap using f2py

https://docs.scipy.org/doc/numpy/user/c-info.python-as-glue.html

example was tested in local directory ~/myfortran/ with add.f
	
### step 1.
	
	$ f2py -h add.pyf -m add add.f
this will leave the add.pyf in the current directory.
	
### step2.
modify declaration of variables by placing intent directives and checking code.
	
### step3.
after modifying add.pyf, the new python module file can be generated by compiling both add.f and add.pyf
	
	$ f2py -c add.pyf add.f
	
	
test in python.
	
	$ python3.5
	>>> import add
	>>> print(add.zadd.__doc__)
	>>> c = add.zadd([1,2,3],[4,5,6])
	
the array created is automatically numpy array.
so we can freely use 
	
	>>> c.shape
and so on!
done!

## fortran_magic in jupyter notebook

https://github.com/mgaitan/fortran_magic

Compile and import symbols from a cell with fortran code, using f2py.

install or upgrade via pip

	pip install -U fortran-magic
	
Once it's installed, you can load it with *%load_ext fortranmagic*. Then put your Fortran code in a cell started with the cell magic *%%fortran*. 

	In[1]: %load_ext fortranmagic
	In[2]: %%fortran
		subroutine f1(x,y,z)
			real, intent(in)  :: x,y
			real, intent(out) :: z
			z = sin(x+y)
		end subroutine f1

[documentation](http://nbviewer.jupyter.org/github/mgaitan/fortran_magic/blob/master/documentation.ipynb)
