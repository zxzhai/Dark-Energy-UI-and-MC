Welcome to DE_Mod_Gen! This piece of software is designed to allow the user to test dynamical dark enery models in the framework of an effective field theory with an arbitrary
number of fields. The following sections of this file will guide you through the setup and use of this program. For further information please reference the paper associated with
this code at (paper url after it has been put on arxiv), and please be sure to reference Hinton et al. and this repository if you use the code in your research.

Section 1: System Requirements

	Software:
		
		The code for DE_Mod_Gen is based on the Python 2.7 build. In order to run the code the user will need several third party modules. These modules are numpy, scipy,
		matplotlib/pylab, and sympy. The first three of these modules are generally included with the major Python distributions, however you will likely need to manually
		install sympy onto your machine.
		
		If you need to install any of the required modules, there is a common and simple way to get them. In the computer command line you will need to type the following
		"python easy_install 'module'"
		where the parantheses are removed and 'module' is the name of the module you would like installed. Note that the name for sympy that must be passed to this argument
		simpy. If this method does not work it is strongly recommended that you download a newer distribution of Python. Third party add ons, such as iPython, may also
		have their own unique ways of installing modules, which should be well documented on their associated web pages.

	Hardware:

		In order to shorten the amount of time that a user must sit waiting for results, the Monte Carlo code provided with DE_Mod_Gen is designed to take full advantage
		of multicore processors. This will put processors under a fair deal of stress, so if your machine gets hot easily or if you are doing other things while running 
		this code it may be best to set the number of processors used by the code to be less than the maximum number available to it. Also, the memory requirements of the
		code should only be several MB, so modern computers should face no difficulty unless you are also running numerous other programs in the background.


Section 2: The Monte Carlo Generator

	Running the Code:

		The Monte Carlo code provided with DE_Mod_Gen has been designed to require as little user input as possible to make it very easy to use. The first entry that you
		will need to provide is the name of the model that you are testing. This name will be used in the user interface to access information about this model. Note that
		if you use the same name as a model that has already been run it will overwrite the fiducial values for that model. Once a name has been selected you must also
		specify how many different initial conditions you would like the code to test. By default this value is set to 10,000, however there are no restrictions on this 
		value other than being a positive integer. After this you must input the equation for g(Y) that uniquely describes the model that you are testing. For a full
		description of what this equation is please reference our paper.

		Once the model has been specified, the range of the initial conditions must be chosen. The first thing to choose is the number of fields that the set of tests will
		be run with. All of the instances of the model with have the same number of fields for each run of the Monte Carlo code. After this the user selects the range of
		initial conditions for several parameters relating to the kinetic and potential energy of the fields. A full description and definition of these parameters is found
		in the paper. Each new universe tested by the code will have its initial conditions generated by selecting a random number from a flat distribution over the 
		selected range of each parameter.

		After the range of the initial conditions is selected, there are two more optional parameters to adjust. The first is the parameter GC. If your model is based on
		ideas similar to the ghost condensate model, there may need to be limits on the ratio between the initial kinetic and potential energy of the fields. By setting
		this parameter to "True", the ratio of x_i/y_i will be randomly selected to be between .5 and sqrt(2). This condition at least allows the model of ghost condensates
		tested by us to run correctly. If you model is not running even with this selection, you can attempt to change this ratio in the monte_pack.py module. After this
		parameter there is also the option to manually select how many processors the tests are distrubuted to. By default the program will use all available processors
		on the machine.

	Data Output:

		When the Monte Carlo code is finished running it will output three files. The first of these files goes into the Parameters folder. This file holds the name and 
		tested initial conditions of the model that you ran. This allows the user interface to run single instances of the model and suggest fiducial values and tested 
		ranges of each parameter. The second file is placed in the Data folder. This file contains all of the initial conditions and output parameters of every model tested
		by the Monte Carlo code that produced results. If any of the models fail to work (such as producing errors or giving values of nan), its results are simply omitted
		from the output file. This will allow you to still analyze the models that do work in the user interface without raising any more errors. The last file that is 
		saved contains values of D/a for each model out to a redshift of z = 20. Currenly this data is not used by the user interface, however if the user is interested
		these data points should be able to be used to interpolate the growth of linear structure in each model.

Section 3: The User Interface

	Intro:

		After a model has been run through the Monte Carlo generator, the user interface will automatically have access to all of the data that was generated. With this the
		user will have two main options. The first is to run a single instance of the model with specifically chosen initial conditions. This will allow the user to see how
		the components of the universe will evolve under those conditions. The second option will be to analyze the bulk data from a run of the Monte Carlo code. This
		will allow the user to be able to determine the most important parameters leading to dark energy in their models. There is also a button on the Home window which
		can open the Monte Carlo code to be used quickly if you have a third party add on such as iPython. If this button does not work for you, you just have to open the
		code manually in whatever program you use to edit code.

	Single Runs:

		If you select to run a single instance of a model, you will need to make several selections. The first selection that you need to make is what model you would like
		to use. By clicking on the drop down menu, a list of all the models having been tested with the Monte Carlo generator will appear. After this is selected you must
		hit the button specified to the right. This will load a set of fiducial values into the parameter fields. These values are the average values from the suggested
		range, which is the range that each of the parameters was tested over in the Monte Carlo code. Within each of these parameter fields, you may also choose to supply
		your own values as well. If the model does not work you will either see a blank graph appear, or nothing at all. If this happens, all you need to do is select new
		parameters.

		On the right hand side of the window you will also see a series of check boxes. First you will need to select whether you want the x axis of the graph to be 
		displayed in either scalefactor a, or redshift z. If you select either none or both of these boxes, a message will remind you to only pick one. Below this you can
		also choose which parameters you would like to see on this graph. The options are the density parameters for dark energy, matter, and radiation, as well as the
		equation of state, w, for dark energy and the linear growth function D/a. You may select as many or as few of these parameters as you would like.

	Results Page:

		From the results page you can analyze the data from a run of the Monte Carlo generator. You are able to make up to two graphs which will appear simultaneously. The
		first step is to select which run you want the data to be pulled from. Each option gives the model name and the number of fields that the models were tested with.
		After a model is selected, you simply need to select what data you would like to see on both the x and y axes of the graphs. The inputs in these fields can be any
		function of the available parameters listed on the window. These functions must be written in Python syntax, and can include either built in Python functions or
		any function from the numpy package using the np. prefix. A full list of numpy functions can be found in the documentaion at http://docs.scipy.org/doc/.