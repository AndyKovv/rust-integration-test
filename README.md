# rust-integration-test
Procedural macros for writing integration tests in rust lang.

Purpose of this project is create multy functional tool for easy create integration tests in rust lang.
At this moment added only set_up() and tear_down() hooks and panic cathing.

If you want add hooks to you integaration test for create_something or remove after you need add #[integration_test] macro after #[test] macro.
When you add #[integration_test] you must add set_up(), and tear_down() hooks.

Example:
```
#[cfg(test)]
pub mod some_test {
   use super::*;
   
   fn set_up() {
     println!("Set up");
   }
   fn tear_down() {
     println!("Tear down");
   }
 
   #[test]
   #[integration_test]
   fn my_shiney_integration_test() {
     asserteq!(1, 2);
   }
}

Expected output order is:
 1) "Set up"`
 2) panic!() -> is going to show after tear_down() finish
 3) "Tear down"
