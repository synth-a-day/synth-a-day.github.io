<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stats Countdown with Progress Bar</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: #000;
            color: #fff;
            margin: 0;
            text-align: center;
        }

        .container {
            margin-bottom: 20px;
        }

        .stats {
            font-size: 24px;
            margin-bottom: 20px;
        }

        .stat {
            margin: 10px 0;
        }

        .soundcloud-player {
            width: 100%;
            max-width: 800px; /* Adjust max-width as needed */
            margin: 20px 0;
        }

        /* Progress Bar Styles */
        .progress-container {
            width: 100%;
            max-width: 800px; /* Adjust max-width as needed */
            background: #333;
            border-radius: 5px;
            overflow: hidden;
            margin: 20px 0;
        }

        .progress-bar {
            height: 20px;
            background: #00ff00;
            width: 100%; /* Initially full width */
            transition: width 0.1s linear;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="stats">
            <div id="commends" class="stat">Commends: 22999</div>
            <div id="matches" class="stat">Matches: 14278</div>
            <div id="wins" class="stat">Wins: 6843</div>
            <div id="mvps" class="stat">MVPs: 325</div>
        </div>
        <div class="progress-container">
            <div id="progress-bar" class="progress-bar"></div>
        </div>
        <div class="soundcloud-player">
            <iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/1872881544&color=%23000000&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>
            <div style="font-size: 10px; color: #cccccc; line-break: anywhere; word-break: normal; overflow: hidden; white-space: nowrap; text-overflow: ellipsis; font-family: Interstate, Lucida Grande, Lucida Sans Unicode, Lucida Sans, Garuda, Verdana, Tahoma, sans-serif; font-weight: 100;">
                <a href="https://soundcloud.com/paulrez" title="Paul Ressel" target="_blank" style="color: #cccccc; text-decoration: none;">Paul Ressel</a> ·
                <a href="https://soundcloud.com/paulrez/dont-worry-youre-not-invited" title="Don't Worry You're Not Invited" target="_blank" style="color: #cccccc; text-decoration: none;">Don't Worry You're Not Invited</a>
            </div>
        </div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Initial stats
            const stats = {
                commends: 22999,
                matches: 14278,
                wins: 6843,
                mvps: 325
            };

            // Elements
            const commendsElem = document.getElementById('commends');
            const matchesElem = document.getElementById('matches');
            const winsElem = document.getElementById('wins');
            const mvpsElem = document.getElementById('mvps');
            const progressBarElem = document.getElementById('progress-bar');

            // Duration in milliseconds
            const duration = 60000; // 1 minute in milliseconds
            const interval = 100; // Update interval in milliseconds
            const totalSteps = duration / interval; // Total number of steps

            // Initial values
            const initialValues = {
                commends: stats.commends,
                matches: stats.matches,
                wins: stats.wins,
                mvps: stats.mvps
            };

            // Calculate decrement per step
            const decrementRates = {
                commends: initialValues.commends / totalSteps,
                matches: initialValues.matches / totalSteps,
                wins: initialValues.wins / totalSteps,
                mvps: initialValues.mvps / totalSteps
            };

            // Update function
            function updateStats() {
                commendsElem.textContent = `Commends: ${Math.max(Math.round(stats.commends), 0)}`;
                matchesElem.textContent = `Matches: ${Math.max(Math.round(stats.matches), 0)}`;
                winsElem.textContent = `Wins: ${Math.max(Math.round(stats.wins), 0)}`;
                mvpsElem.textContent = `MVPs: ${Math.max(Math.round(stats.mvps), 0)}`;
            }

            // Countdown function
            function countdown() {
                if (stats.commends > 0 || stats.matches > 0 || stats.wins > 0 || stats.mvps > 0) {
                    if (stats.commends > 0) stats.commends -= decrementRates.commends;
                    if (stats.matches > 0) stats.matches -= decrementRates.matches;
                    if (stats.wins > 0) stats.wins -= decrementRates.wins;
                    if (stats.mvps > 0) stats.mvps -= decrementRates.mvps;

                    updateStats();

                    // Update progress bar
                    const progress = ((initialValues.commends - stats.commends) / initialValues.commends) * 100;
                    progressBarElem.style.width = `${progress}%`;

                    setTimeout(countdown, interval); // Update every interval milliseconds
                }
            }

            updateStats(); // Initial update
            countdown(); // Start countdown
        });
    </script>
</body>
</html>
# synth-a-day.github.io
synth-a-day
