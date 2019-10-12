# CSS-Clock
An analogue clock built with HTML, CSS and plain Javascript

<script>
        const time = new Date();
        const second = time.getSeconds();
        const minute = time.getMinutes() + (second / 60);
        let hour = time.getHours() + (minute / 60);
        if (hour > 12) {
            hour = hour - 12;
        }
        document.documentElement.style.setProperty('--start-seconds', second);
        document.documentElement.style.setProperty('--start-minutes', minute);
        document.documentElement.style.setProperty('--start-hours', hour);
    </script>
    <style>
        body {
            width: 100vw;
            height: 100vh;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            min-width: var(--clock-diameter);
        }
        .clockFace {
            --clock-diameter: 50vw;
            font-size: 4vw;
            width: var(--clock-diameter);
            height: var(--clock-diameter);
            border-radius: 50%;
            background-color: black;
            color: white;
            box-sizing: border-box;
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .hand {
            box-sizing: border-box;
            position: absolute;
        }
        .secondHand {
            width: 40%;
            height: 2px;
            background: red;
            border-radius: 1px;
            transform: rotate(calc(var(--start-seconds) * 6deg + 90deg)) translate(-50%, 0px);
            animation: rotateSecondsHand 60s steps(60) infinite;
        }
        .minuteHand {
            width: 35%;
            height: 4px;
            background-color: cyan;
            border-radius: 2px;
            transform: rotate(calc(var(--start-minutes) * 6deg + 90deg)) translate(-50%, 0px);
            animation: rotateMinutesHand 3600s steps(600) infinite;
            animation-delay: calc(var(--start-seconds) * -1 * 1s);
        }
        .hourHand {
            width: 30%;
            height: 8px;
            background: green;
            border-radius: 4px;
            transform: rotate(calc(var(--start-hours) * 30deg + 90deg)) translate(-50%, 0px);
            animation: rotateHoursHand calc(12 * 60 * 60s) steps(600) linear infinite;
            animation-delay: calc(calc(var(--start-minutes) * -60 * 1s) + calc(var(--start-seconds) * -1 * 1s));
        }
        @keyframes rotateSecondsHand {
            from {
                transform: rotate(calc(var(--start-seconds) * 6deg + 90deg)) translate(-50%, 0px);
            }
            to {
                transform: rotate(calc(var(--start-seconds) * 6deg + 450deg)) translate(-50%, 0px);
            }
        }
        @keyframes rotateMinutesHand {
            from {
                transform: rotate(calc(var(--start-minutes) * 6deg + 90deg)) translate(-50%, 0px);
            }
            to {
                transform: rotate(calc(var(--start-minutes) * 6deg + 450deg)) translate(-50%, 0px);
            }
        }
        @keyframes rotateHoursHand {
            from {
                transform: rotate(calc(var(--start-hours) * 30deg + 90deg)) translate(-50%, 0px);
            }
            to {
                transform: rotate(calc(var(--start-hours) * 30deg + 450deg)) translate(-50%, 0px);
            }
        }
    </style>
    <body>
    <div class="container">
        <div class="clockFace">
            <div style="position: absolute; top: 0;">12</div>
            <div style="position: absolute; right: 0">3</div>
            <div style="position: absolute; bottom: 0;">6</div>
            <div style="position: absolute; left: 0;">9</div>
            <div class="hand hourHand"></div>
            <div class="hand minuteHand"></div>
            <div class="hand secondHand"></div>
        </div>
    </div>
</body>
