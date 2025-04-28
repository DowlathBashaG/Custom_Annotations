# Custom_Annotations

Custom Annotation :

Step by Step :

Step 1: Define the custom annotation 

		import java.lang.annotation.*
		
		@Retention(RetentionPolicy.RUNTIME)
		@Target({ElementType.Type, ElementType.Method})
		public @interface MyAnnotation {
			String author() default "Unknown";
			String purpose() defualt "No purpose specified";
		}

Step 2: Apply annotation to a class and its method 

        
		@MyAnnotation(author = "Dowlath Basha G", purpose = "MyAnnotationClass ")
		public class MyAnnotationClass{
		
		@MyAnnotation(author = "Dowlath Basha G", purpose = "This Method says Hello")
		public void sayHello(){
		  System.out.println("Hello from sayHello()");
		}
		
		@MyAnnotation(purpose = "This method is test method")
		public void testMethod(){
		  System.out.println("Inside Test Method()");
		}
		
		public void  noAnnotationMethod(){
		  System.out.println("This method has no annotation"
		}
		}


Step 3: Read the annotations using reflection
        
	public class AnnotationProcessor {
    public static void main(String args[]) {
        // Class level annotation
        Class<MyAnnotationClass> obj = MyAnnotationClass.class;

        if (obj.isAnnotationPresent(MyAnnotation.class)) {
            MyAnnotation myAnnotation = obj.getAnnotation(MyAnnotation.class);
            System.out.println("Class Annotation:");
            System.out.println("Author: " + myAnnotation.author());
            System.out.println("Purpose: " + myAnnotation.purpose());
            System.out.println("-------------------------------------------------");

            // Process method-level annotations
            for (Method method : obj.getDeclaredMethods()) {
                if (method.isAnnotationPresent(MyAnnotation.class)) {
                    MyAnnotation info = method.getAnnotation(MyAnnotation.class);
                    System.out.println("Method: " + method.getName());
                    System.out.println("Author: " + info.author());
                    System.out.println("Purpose: " + info.purpose());
                    System.out.println("--------------------------");
                }
            }
        }
    }
}
		
	Output :
	
	Class Annotation:
	Author: John Doe
	Purpose: Demo Class
	--------------------------
	Method: sayHello
	Author: John Doe
	Purpose: This method says hello
	--------------------------
	Method: testMethod
	Author: Unknown
	Purpose: Just a test method
	--------------------------


		
		
		  
