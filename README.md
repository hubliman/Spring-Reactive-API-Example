Spring Reactive API Example:

This project is example of API endpoint with Reactive Support. This is an example to make a demo of API endpoint which return/emit resource every second.


[1] How to create project:
    Go to https://start.spring.io/. 
	[a] Select Build Tool as Maven
	[b] Langauage : Java
	[c] Spring Boot Version: 2.7.7
	[d] Add Dependencies : Spring Boot DevTools, Spring Reactive Web
	[e] Click on Generate

[2] create foo class with properties id and name with Lombok annotations
    
	package com.example.demo;

	import lombok.AllArgsConstructor;
	import lombok.EqualsAndHashCode;
	import lombok.Getter;
	import lombok.NoArgsConstructor;
	import lombok.RequiredArgsConstructor;
	import lombok.Setter;

	@Getter
	@Setter
	@EqualsAndHashCode
	@NoArgsConstructor
	@AllArgsConstructor


	public class foo {
		private int id;
		private String name;
	}
	
[3] Create REST Endpoint

    package com.example.demo;

import java.time.Duration;

import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Flux;

@RestController
public class foocontroller {

    foo[] foos = new foo[50] ;

    public foocontroller (){

        
        foos[0] = new foo(1,"One");  
        foos[1] = new foo(2,"Two");  
        foos[2] = new foo(3,"Three");  
        foos[3] = new foo(4,"Four");  
        foos[4] = new foo(5,"Five");  
        foos[5] = new foo(6,"Six");  
        foos[6] = new foo(7,"Seven");  
        foos[7] = new foo(8,"Eight");  
        foos[8] = new foo(9,"Nine");  
        foos[9] = new foo(10,"Ten");  
        foos[10] = new foo(11,"Elven");  
        foos[11] = new foo(12,"Twelve");  
        foos[12] = new foo(13,"Thirteen");  
        foos[13] = new foo(14,"Fourteen");  
        foos[14] = new foo(15,"Fifteen");  
        foos[15] = new foo(16,"Sixteen");  
        foos[16] = new foo(17,"Seventeen");  
        foos[17] = new foo(18,"Eighteen");  
        foos[18] = new foo(19,"Nineteen");  
        foos[19] = new foo(20,"Twenty");  
        foos[20] = new foo(21,"Twentyone");  

    }
   

	@GetMapping(value="/foos", produces = MediaType.TEXT_EVENT_STREAM_VALUE)
	public Flux<foo> getFoos() {
		return Flux
            .just(foos)
            .delayElements(Duration.ofSeconds(1))
            .repeat()
            .log();
	}

	}
	
[4] How to Run Project: 
    
	[a] Open commandline and go to folder of the project
	[b] Run the command: mvn install
	[c] Run project by excecuting the command: mvn exec:java -Dexec.mainClass=com.example.demo.DemoApplication
	
[5] How to Test the output.

    Open browser: Enter the following URL: http://localhost:8080/foos
