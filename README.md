# EXP4.1-23BCS13917

const readline = require('readline');

// In-memory array to store employees
let employees = [];

// Create CLI interface
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

function mainMenu() {
  console.log(`
=============================
 Employee Management System
=============================
1. Add Employee
2. View All Employees
3. Update Employee
4. Delete Employee
5. Search Employee by ID
6. Exit
  `);
  rl.question('Choose an option: ', (choice) => {
    switch (choice.trim()) {
      case '1':
        addEmployee();
        break;
      case '2':
        viewEmployees();
        break;
      case '3':
        updateEmployee();
        break;
      case '4':
        deleteEmployee();
        break;
      case '5':
        searchEmployee();
        break;
      case '6':
        console.log('Exiting...');
        rl.close();
        break;
      default:
        console.log('Invalid choice');
        mainMenu();
    }
  });
}

function addEmployee() {
  rl.question('Enter Employee ID: ', (id) => {
    rl.question('Enter Name: ', (name) => {
      rl.question('Enter Position: ', (position) => {
        employees.push({ id, name, position });
        console.log('✅ Employee added successfully!');
        mainMenu();
      });
    });
  });
}

function viewEmployees() {
  console.log('\n=== All Employees ===');
  if (employees.length === 0) {
    console.log('No employees found.');
  } else {
    employees.forEach((emp, index) => {
      console.log(`${index + 1}. ID: ${emp.id}, Name: ${emp.name}, Position: ${emp.position}`);
    });
  }
  mainMenu();
}

function updateEmployee() {
  rl.question('Enter Employee ID to update: ', (id) => {
    let emp = employees.find(e => e.id === id);
    if (!emp) {
      console.log('❌ Employee not found.');
      return mainMenu();
    }
    rl.question(`Enter New Name (${emp.name}): `, (name) => {
      rl.question(`Enter New Position (${emp.position}): `, (position) => {
        emp.name = name || emp.name;
        emp.position = position || emp.position;
        console.log('✅ Employee updated!');
        mainMenu();
      });
    });
  });
}

function deleteEmployee() {
  rl.question('Enter Employee ID to delete: ', (id) => {
    let index = employees.findIndex(e => e.id === id);
    if (index === -1) {
      console.log('❌ Employee not found.');
    } else {
      employees.splice(index, 1);
      console.log('✅ Employee deleted!');
    }
    mainMenu();
  });
}

function searchEmployee() {
  rl.question('Enter Employee ID to search: ', (id) => {
    let emp = employees.find(e => e.id === id);
    if (emp) {
      console.log(`Found: ID: ${emp.id}, Name: ${emp.name}, Position: ${emp.position}`);
    } else {
      console.log('❌ Employee not found.');
    }
    mainMenu();
  });
}

mainMenu();
