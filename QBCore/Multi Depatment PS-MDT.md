how to add multi jobs to ps-mdt

app.js

copy and paste 
Line 29

```
// TEMP CONFIG OF JOBS
const PoliceJobs = {
  ['police']: true,
  ['lspd']: true,
  ['bcso']: true,
  ['sast']: true,
  ['sasp']: true, 
}
```

line 4075

```
if (PoliceJobs[unit.unitType] !== undefined) {
          policeCount++;
          if (unit.unitType == "police") {
            activeInfoJob = `<div class="unit-job active-info-job-lspd">LSPD</div>`;
          } else if(unit.unitType == "bcso")  {
            activeInfoJob = `<div class="unit-job active-info-job-bcso">BCSO</div>`;
          } else if(unit.unitType == "sasp")  {
            activeInfoJob = `<div class="unit-job active-info-job-sasp">SASP</div>`;
          } else if(unit.unitType == "judge")  {
            activeInfoJob = `<div class="unit-job active-info-job-doj">DOJ</div>`;
          }
        } else if (AmbulanceJobs[unit.unitType] !== undefined) {
          activeInfoJob = `<div class="unit-job active-info-job-ambulance">Ambulance</div>`
          emsCount++;
        /* } else if  (DojJobs[unit.unitType] !== undefined) {
          activeInfoJob = `<div class="unit-job active-info-job-fire">FIRE</div>`
          fireCount++; */
        } else if (DojJobs[unit.unitType] !== undefined) {
          activeInfoJob = `<div class="unit-job active-info-job-doj">DOJ</div>`
          dojCount++; 
        }
```

then go to 

Dashboard.html
line 194

```
<div class="active-unit-title">Active Units</div>
                    <div class="active-unit-count" id="police-count">0</div>
                    <div class="active-unit-count" id="bcso-count">0</div> 
                    <div class="active-unit-count" id="sasp-count">0</div>
                    <div class="active-unit-count" id="ems-count">0</div>
                    <div class="active-unit-count" id="doj-count">0</div>
                    <div class="active-unit-count" id="fire-count">0</div> 
```








Active Unit Fix

Line 4085 
```
      let policeCount = 0;
      let saspCount = 0;
      let bcsoCount = 0;
      let emsCount = 0;
      let dojCount = 0;
      let fireCount = 0;
```
and this at Line 4143
```
      $("#police-count").html(policeCount);
      $("#sasp-count").html(saspCount);
      $("#bcso-count").html(bcsoCount);
      $("#ems-count").html(emsCount);
      $("#doj-count").html(dojCount);
      $("#fire-count").html(fireCount);
```

then you need to add the counter to your jobs like this
```
if (PoliceJobs[unit.unitType] !== undefined) {
          if (unit.unitType == "police") { policeCount++;
            activeInfoJob = `<div class="unit-job active-info-job-lspd">LSPD</div>`;
          } else if(unit.unitType == "bcso")  { bcsoCount++;
            activeInfoJob = `<div class="unit-job active-info-job-bcso">BCSO</div>`;
          } else if(unit.unitType == "sasp")  { saspCount++;
            activeInfoJob = `<div class="unit-job active-info-job-sasp">SASP</div>`;
          } else if(unit.unitType == "judge")  { dojCount++;
            activeInfoJob = `<div class="unit-job active-info-job-doj">DOJ</div>`;
          }
        } else if (AmbulanceJobs[unit.unitType] !== undefined) {
          activeInfoJob = `<div class="unit-job active-info-job-ambulance">Ambulance</div>`
          emsCount++;
        /* } else if  (DojJobs[unit.unitType] !== undefined) {
          activeInfoJob = `<div class="unit-job active-info-job-fire">FIRE</div>`
          fireCount++; */
        } else if (DojJobs[unit.unitType] !== undefined) {
          activeInfoJob = `<div class="unit-job active-info-job-doj">DOJ</div>`
          dojCount++; 
        }
```

this SHOULD make the counters work im tesing RN still 
to add the color to the active unit boxes after police-count on Line 571 Add this 

In css
```
#sasp-count {
    background-color: #2589cc;
}

#bcso-count {
    background-color: #cc7e25;
}
```