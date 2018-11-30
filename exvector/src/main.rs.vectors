const SDR_LENGTH: usize = 21;
const INPUT_LENGTH: usize = 819;

pub struct Column {
    sdr: Vec<usize>,
    input: Vec<usize>,
    result: Vec<usize>
}

fn main() {
    let mut columns: Vec<Column> = (0..1024).map(|i| init_column()).collect();
    columns.iter_mut().for_each(|c| intersection(c));
    columns.iter().for_each(|c|report(c));

    0;
}

fn init_column() -> Column {
    Column {
        sdr: (0 .. SDR_LENGTH).map(|i| INPUT_LENGTH - i).collect(),
        input: (0 .. INPUT_LENGTH).map(|i| INPUT_LENGTH - i).collect(),
        result: Vec::new()
    }

}


fn intersection(c: &mut Column) {
    c.input.sort();
    c.sdr.sort();


    let mut i = 0;
    let mut s = 0;

    while i < INPUT_LENGTH && s < SDR_LENGTH {
        if c.input[i] < c.sdr[s] {
            i += 1;
        } else if c.input[i] > c.sdr[s] {
            s += 1;
        } else {
            c.result.push(c.input[i]);
            i += 1;
            s += 1;
        }
    }

}

fn report(c: &Column) {
    println!("The intersection has {} elements:", c.result.len());
    c.result.iter().for_each(|c| { print!(" {}", c); });
    println!();
}
