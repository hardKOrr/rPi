# newMultiPi.md

# Magic Mirror
```
cd ~/
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt install -y nodejs
git clone https://github.com/MichMich/MagicMirror
cd MagicMirror/
npm install
```
```
cd ~/MagicMirror/modules
git clone https://github.com/jasonyork/MMM-auto-refresh.git
cd MMM-auto-refresh
npm install
cd ..
```
```
git clone https://github.com/MMM-CalendarExt2/MMM-CalendarExt2.git
cd MMM-CalendarExt2
npm install
cd ..
```
```
git clone https://github.com/jclarke0000/MMM-DarkSkyForecast.git
cd MMM-DarkSkyForecast
npm install
cd ..
```
```
git clone https://github.com/gubbsjuk/MMM-GoogleTasks.git
cd MMM-GoogleTasks
npm install
cd ..
```
```
git clone https://github.com/NolanKingdon/MMM-MoonPhase.git
cd MMM-MoonPhase
npm install
cd ..
```
```
git clone https://github.com/pinsdorf/MMM-WeeklySchedule.git
cd MMM-WeeklySchedule
npm install
cd ~/
```
```
pm2 restart mm
```
