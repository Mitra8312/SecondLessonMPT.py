<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Поисковое приложение</title>
    
    <!-- Подключение Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
        }
        
        .container {
            display: flex;
            flex-direction: column;
            gap: 20px;
            max-width: 800px;
            margin: 0 auto;
        }
        
        .search-row {
            display: flex;
            justify-content: space-between;
            gap: 10px;
            align-items: center;
        }

        .search-row input[type="text"] {
            flex-grow: 1;
        }
        
        .table-container {
            display: flex;
            justify-content: space-between;
            gap: 20px;
        }
        
        .table-wrapper {
            width: 100%;
            max-height: 300px;
            overflow-y: auto;
            border: 1px solid #ddd;
            padding: 10px;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
        }
        
        table th, table td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }

        table th {
            background-color: #f4f4f4;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="search-row">
        <!-- Выпадающий список слева -->
        <select id="left-dropdown" class="form-select">
            <option value="option1">Вариант 1</option>
            <option value="option2">Вариант 2</option>
        </select>

        <!-- Поле для ввода поиска -->
        <input type="text" id="search-input" class="form-control" placeholder="Введите запрос...">

        <!-- Выпадающий список справа -->
        <select id="right-dropdown" class="form-select">
            <option value="option1">Вариант A</option>
            <option value="option2">Вариант B</option>
            <option value="option3">Вариант C</option>
        </select>

        <!-- Кнопка поиска -->
        <button class="btn btn-primary" onclick="performSearch()">Поиск</button>
    </div>

    <!-- Контейнеры для таблиц -->
    <div class="table-container">
        <div class="table-wrapper">
            <table id="table1" class="table table-striped table-bordered">
                <thead>
                    <tr>
                        <th>Заголовок 1</th>
                        <th>Заголовок 2</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Данные таблицы 1 -->
                </tbody>
            </table>
        </div>

        <div class="table-wrapper">
            <table id="table2" class="table table-striped table-bordered">
                <thead>
                    <tr>
                        <th>Заголовок 1</th>
                        <th>Заголовок 2</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Данные таблицы 2 -->
                </tbody>
            </table>
        </div>
    </div>
</div>

<!-- Подключение Bootstrap JS и зависимости -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>

<script>
    // Функция для выполнения поиска
    function performSearch() {
        const leftDropdownValue = document.getElementById("left-dropdown").value;
        const searchQuery = document.getElementById("search-input").value;
        const rightDropdownValue = document.getElementById("right-dropdown").value;

        // Пример вызова API для получения данных
        fetchTableData('https://api.example.com/data1', 'table1');
        fetchTableData('https://api.example.com/data2', 'table2');
    }

    // Функция для выполнения запроса к API и заполнения таблицы
    function fetchTableData(apiUrl, tableId) {
        // Пример использования fetch для получения данных с API
        fetch(apiUrl)
            .then(response => response.json())
            .then(data => {
                const tableBody = document.querySelector(`#${tableId} tbody`);
                tableBody.innerHTML = ''; // Очистка текущих данных таблицы

                data.forEach(item => {
                    const row = document.createElement('tr');
                    const cell1 = document.createElement('td');
                    const cell2 = document.createElement('td');

                    cell1.textContent = item.field1; // Пример поля 1
                    cell2.textContent = item.field2; // Пример поля 2

                    row.appendChild(cell1);
                    row.appendChild(cell2);
                    tableBody.appendChild(row);
                });
            })
            .catch(error => {
                console.error('Ошибка при запросе данных:', error);
            });
    }
</script>

</body>
</html>
