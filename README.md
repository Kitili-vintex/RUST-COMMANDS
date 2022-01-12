use::std::io;
use std::collections::HashMap;

fn main() {



    let mut names = Vec::new();
    let mut departments = Vec::new();
    let mut directory = HashMap::new();


    loop {
        println!("Welcome to our company tech sevices");


        println!("Here are the departments in our company {:#?}", departments);

        println!("Do you want to:
              a)Add another person & department, 
              b)View department,
              c)View all,
              d)Exit");     


        let mut yn = String::new();
        io::stdin().read_line(&mut yn).expect("Failed to read line");
        match yn.trim() {
            "a" => {
                let mut name = String::new();
                let mut department = String::new();
                println!("Input first and last name");
                io::stdin()
                    .read_line(&mut name)
                    .expect("Failed to read line");

                println!("What department does {} work in?", name. to_uppercase());
                io::stdin()
                    .read_line(&mut department)
                    .expect("Failed to read line");

                departments.push(department.trim().to_string().to_uppercase());
                names.push(name.trim().to_string());

                directory
                    .entry(department.trim().to_string())
                    .or_insert_with(Vec::new)
                    .push(name.trim().to_string().to_uppercase());

            }
            "b" => {
                println!(
                    "Which department would you like to see?"
                );
                let mut x = String::new();

                io::stdin()
                    .read_line(&mut x)
                    .expect("Failed to read line");
                println!("These people work in {:#?}: => {:#?}", &x.trim().to_string().to_uppercase(), directory.get(&x.trim().to_string()));

            }
            "c" => {
                println!(
"These are all the people in our company => {:#?}
These are all the departments in our company => {:#?}.",
                    names, departments);
            }
            "d" => break,
            _ => {
                println!("You typed {}", yn.to_uppercase());
            }
        }
}    } 
