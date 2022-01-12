pub fn from(w: &str) -> Option<String> {
    if w.is_empty() {

        return Some(String::new());
    }

    let first_byte = w.as_bytes()[0];
    if !first_byte.is_ascii_alphabetic() {
        return None;
    }

    let vowels = b"abeiou";
    if vowels.contains(&first_byte.to_ascii_lowercase()) {
        return Some(format!("{}-hay", w));
    }

    let (first_letter,suffix) =  w.split_at(1);
    Some(format!("{}-{}ay",suffix,first_letter))
}
fn main() {} 

