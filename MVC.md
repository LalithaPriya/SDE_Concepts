# MVC

The MVC architecture pattern turns complex application development into a much more manageable process. It allows several developers to simultaneously work on the application.

MVC stands for model-view-controller. Here's what each of those components mean:

Model: The backend that contains all the data logic
View: The frontend or graphical user interface (GUI)
Controller: The brains of the application that controls how data is displayed.

- The model's job is to simply manage the data. Whether the data is from a database, API, or a JSON object, the model is responsible for managing it.

- The view's job is to decide what the user will see on their screen, and how.

- The controller's responsibility is to pull, modify, and provide data to the user. Essentially, the controller is the link between the view and model.Through getter and setter functions, the controller pulls data from the model and initializes the views.

Some of the early frameworks that applied these concepts were Angular, KnockoutJS, Django, and Ruby on Rails.



