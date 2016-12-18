# GAelectrodynamics
A book on Geometric Algebra applications to electromagnetism

To access, and build the this book from the latex run:

   mkdir ~/project
   cd ~/project/
   touch METADATA
   chmod 755 METADATA
   git clone git@github.com:peeterjoot/GAelectrodynamics.git
   git clone git@github.com:peeterjoot/latex.git
   git clone git@github.com:peeterjoot/GAelectrodynamicsFigures.git figures

   # or
   git clone https://github.com/peeterjoot/GAelectrodynamics.git
   git clone https://github.com/peeterjoot/latex.git
   git clone https://github.com/peeterjoot/GAelectrodynamicsFigures.git figures

   cd GAelectrodynamics
   make

Then add:

   PATH=$PATH:~/project/latex/bin

to your .profile 
