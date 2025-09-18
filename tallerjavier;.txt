use employees;
select * from employees;
1select  count(emp_no) from employees; 
2select max(salary) as salario_maximo , min(salary) as salario_minimo  from salaries;
3select avg(salary)  as promedio_salario from salaries;
4select gender, count(*) from employees group by gender;
5select count(title),title from titles group by title;
6SELECT title, COUNT(*) FROM titles GROUP BY title HAVING COUNT(*) > 75000;
7select count(gender) as total_empleados,titles.title,gender from employees join titles on employees.emp_no=titles.emp_no group by gender,title;
8select e.emp_no,e.first_name, dd.dept_name from employees e left join dept_emp d on e.emp_no=d.emp_no left join  departments dd on d.dept_no=dd.dept_no;
9select employees.first_name,employees.last_name from employees join dept_emp on employees.emp_no=dept_emp.emp_no 
join departments on dept_emp.dept_no=departments.dept_no
where departments.dept_name="marketing";
10select p.emp_no, concat(p.first_name,'',p.last_name) as nombre_completo,
 de.dept_name , t.title from employees p join dept_manager d on p.emp_no=d.emp_no join titles t on p.emp_no=t.emp_no
 join departments de on d.dept_no=de.dept_no where t.title="manager";
 11select dep.dept_name , avg(sa.salary) as salariopromedio from dept_emp de join employees em on de.emp_no=em.emp_no 
 join salaries sa on sa.emp_no=em.emp_no join departments dep on dep.dept_no=de.dept_no group by dep.dept_name;
 12select e.emp_no ,t.title,t.from_date,t.to_date from titles t join employees e on e.emp_no=t.emp_no where e.emp_no=10006;
 13select dep.dept_name  from departments dep  left join  dept_emp  d on d.dept_no=dep.dept_no  left join employees e
 on e.emp_no=d.emp_no where d.emp_no is null group by d.emp_no;
14 select e.first_name,e.last_name, s.salary from employees e join salaries s on e.emp_no=s.emp_no group by e.emp_no;
15select emp_no from salaries where salary>(select avg(salaries.salary) as salariopromedio from salaries) group by emp_no; 
16select first_name,last_name from employees where emp_no in (select emp_no from titles  where title='manager');
17select first_name,last_name from employees where emp_no not in (select emp_no from titles  where title='manager');
18select first_name,last_name,hire_date from employees order by hire_date desc limit 1;
19 select e.first_name from employees e join titles t on e.emp_no=t.emp_no join dept_manager dept on t.emp_no=dept.emp_no join departments dep on dept.dept_no=dep.dept_no where dep.dept_name='development' group by t.emp_no; 
20select emp_no,salary from salaries order by salary desc;
21 SELECT CONCAT(first_name, ' ', last_name) AS nombre_completo FROM employees LIMIT 100;
22SELECT emp_no,TIMESTAMPDIFF(YEAR, hire_date, CURDATE()) AS antiguedad_en_años FROM employees;
23SELECT employees.first_name,salaries.salary,
    CASE
        WHEN salaries.salary < 50000 THEN 'Bajo'
        WHEN salaries.salary BETWEEN 50000 AND 90000 THEN 'Medio'
        WHEN salaries.salary > 90000 THEN 'Alto'
        ELSE 'No especificado' -- Opcional: Para salarios que no cumplen ninguna condición
    END AS categoria_salario
FROM
    employees,salaries;
  24 SELECT
    EXTRACT(MONTH FROM birth_date) AS mes_contratacion, -- O `MONTH(fecha_contratacion)` dependiendo del dialecto SQL
    COUNT(*) AS cantidad_empleados
FROM
    employees -- Reemplaza `Empleados` con el nombre de tu tabla de empleados
WHERE
    birth_date IS NOT NULL -- Opcional: para excluir empleados sin fecha de contratación
GROUP BY
    mes_contratacion;       
25 SELECT
    first_name,
    last_name,
    CONCAT(
        SUBSTRING(first_name, 1, 1),
        SUBSTRING(last_name, 1, 1)
    ) AS Iniciales
FROM
    employees;
26 SELECT
	d.dept_name,
    AVG(salary) AS salario_promedio
FROM
    salaries s
    join dept_emp dd on s.emp_no=dd.emp_no
    join departments d on dd.dept_no=d.dept_no
GROUP BY
    d.dept_name
ORDER BY
    salario_promedio DESC
LIMIT 1;
 27 SELECT e.first_name, DATEDIFF(NOW(), e.birth_date) AS dias_en_cargo FROM employees e JOIN titles t ON e.emp_no = t.emp_no WHERE
t.title = 'manager' AND t.emp_no = e.emp_no ORDER BY dias_en_cargo DESC LIMIT 1;
28 select (select salary  as salario_actual from salaries  where emp_no=10001 order by to_date desc limit  1)-(select salary  as primer_salario from salaries where emp_no=10001 order by to_date asc limit  1) as diferencia_salarial;

30select e.emp_no, e.first_name,e.last_name ,max(s.salary) from employees e join salaries s on e.emp_no=s.emp_no join titles t on s.emp_no=t.emp_no where t.title='senior engineer' order by e.emp_no, max(s.from_date);

