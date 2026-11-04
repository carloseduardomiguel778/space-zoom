# space-zoom
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minha Lista de Tarefas</title>
    <style>
        :root {
            --primary-color: #6366f1;
            --primary-hover: #4f46e5;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-color: #1e293b;
            --border-color: #e2e8f0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            background: var(--card-bg);
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
            width: 100%;
            max-width: 400px;
        }

        h1 {
            margin-top: 0;
            font-size: 1.5rem;
            text-align: center;
            color: var(--text-color);
            margin-bottom: 1.5rem;
        }

        .input-group {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 1.5rem;
        }

        input[type="text"] {
            flex: 1;
            padding: 0.75rem;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
            transition: border-color 0.2s;
        }

        input[type="text"]:focus {
            border-color: var(--primary-color);
        }

        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 0.75rem 1.25rem;
            border-radius: 8px;
            font-size: 1rem;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        button:hover {
            background-color: var(--primary-hover);
        }

        ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.75rem;
            border-bottom: 1px solid var(--border-color);
            animation: fadeIn 0.3s ease;
        }

        li:last-child {
            border-bottom: none;
        }

        li span {
            cursor: pointer;
            flex: 1;
            word-break: break-word;
        }

        li.completed span {
            text-decoration: line-through;
            color: #94a3b8;
        }

        .delete-btn {
            background: transparent;
            color: #ef4444;
            padding: 0.25rem 0.5rem;
            font-size: 0.85rem;
        }

        .delete-btn:hover {
            background: #fee2e2;
            color: #dc2626;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-5px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Lista de Tarefas</h1>
        <div class="input-group">
            <input type="text" id="taskInput" placeholder="O que você precisa fazer?">
            <button id="addBtn">Adicionar</button>
        </div>
        <ul id="taskList"></ul>
    </div>

    <script>
        const taskInput = document.getElementById('taskInput');
        const addBtn = document.getElementById('addBtn');
        const taskList = document.getElementById('taskList');

        // Função para adicionar nova tarefa
        function addTask() {
            const text = taskInput.value.trim();
            if (text === '') return;

            const li = document.createElement('li');
            
            const span = document.createElement('span');
            span.textContent = text;
            span.addEventListener('click', () => {
                li.classList.toggle('completed');
            });

            const deleteBtn = document.createElement('button');
            deleteBtn.textContent = 'Excluir';
            deleteBtn.className = 'delete-btn';
            deleteBtn.addEventListener('click', () => {
                li.remove();
            });

            li.appendChild(span);
            li.appendChild(deleteBtn);
            taskList.appendChild(li);

            taskInput.value = '';
            taskInput.focus();
        }

        // Eventos de clique e tecla Enter
        addBtn.addEventListener('click', addTask);
        taskInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                addTask();
            }
        });
    </script>

</body>
</html>
