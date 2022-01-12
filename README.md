use std::collections::HashMap;

pub fn main() {
    let v: Vec<i32> = vec![43, 13, 79, 50, 25, 47, 79, 98, 79];

    match calc_avg(&v) {
        Some(result) => { println!("Mean is {}", result)},
        None => { println!("Mean undefined for {:?}", v);}
    }

    match calc_median(&v) {
        Some(result) => { println!("Median is {}", result)},
        None => { println!("Median undefined for {:?}", v);}
    }

    match calc_mode( &v ) {
        Some(value) => { println!("Mode is {}",value) },
        None => { println!("Mode undefined for {:?}", v);}
    }
}

pub fn calc_avg( l: &Vec<i32> ) -> Option<f64> {
    let sum: i32 = l.iter().sum();
    let len: f64 = l.len() as f64;
    if l.len() > 0 {
        return Some(sum as f64 /len);
    }
    else {
        return None
    }
}
pub fn calc_median( x: &Vec<i32> ) -> Option<f64> {
    let mut l = x.clone();
    l.sort();

    let middle_id = l.len()/2;
    match l.get(middle_id) {
        Some(i) => {
            let mut median = *i as f64;
            if l.len() % 2 == 0 {

                median += l[middle_id-1] as f64;
                median = median / 2.0;
            }
            return Some(median);
        }
        _ => return None
    }
}


pub fn calc_mode( x: &Vec<i32>  ) -> Option<i32> {
    // add keys to a hashmap and keep counts as values
    let mut m = HashMap::new();
    for i in x {
        let count = m.entry(i).or_insert(0);
        *count += 1;
    }

    let mut highest_count = 0;
    let mut highkey = 0;
    let mut valid = true;

    for (key,value) in m {
        if value > highest_count {
            highest_count = value;
            highkey = *key;
            valid = true;
        }
        else if value == highest_count {
            valid = false;
        }
    }

    if highest_count >= 0 && valid == true {
        Some(highkey)
    } 
    else {
        None
    }    
}
