## Replicate tslint bug

(As of 8/14/2017)

Assuming you have the latest version of the Code Climate CLI installed.

*N.B.*
The Code Climate CLI seems to have a bug related to engines which don't have a `latest` channel.

To work around this, I did the following:

1. Manually pulled down the `beta` channel for `tslint`: `docker pull codeclimate/codeclimate-tslint:beta`
1. Tagged `beta` as `latest` so that there's a latest: `docker tag codeclimate/codeclimate-tslint:beta codeclimate/codeclimate-tslint:latest`

## Reproduction

1. Follow instructions above
1. Clone this repository
1. Run `codeclimate analyze`

    You should see output that notes "rule named no-invalid-template-strings is not found"

    The full output however is below:

```
Starting analysis
Running tslint: Failed

Analysis failed with the following output:
tslint:beta produced invalid output: File does not exist: ''; Path is not a file: ''; Path must be present: `{"type"=>"issue", "check_name"=>"(runtime error)", "description"=>"Error: rule named no-invalid-template-strings is not found.\nError: rule named no-invalid-template-strings is not found.\n    at IssueConverter.contentBody (/usr/src/app/dist/issueConverter.js:41:19)\n    at IssueConverter.convert (/usr/src/app/dist/issueConverter.js:27:28)\n    at MapSubscriber._next (/usr/src/app/node_modules/rxjs/operator/map.js:77:35)\n    at MapSubscriber.Subscriber.next (/usr/src/app/node_modules/rxjs/Subscriber.js:89:18)\n    at ArrayObservable._subscribe (/usr/src/app/node_modules/rxjs/observable/ArrayObservable.js:114:28)\n    at ArrayObservable.Observable._trySubscribe (/usr/src/app/node_modules/rxjs/Observable.js:57:25)\n    at ArrayObservable.Observable.subscribe (/usr/src/app/node_modules/rxjs/Observable.js:45:27)\n    at MapOperator.call (/usr/src/app/node_modules/rxjs/operator/map.js:54:23)\n    at Observable.subscribe (/usr/src/app/node_modules/rxjs/Observable.js:42:22)\n    at CatchOperator.call (/usr/src/app/node_modules/rxjs/operator/catch.js:79:23)", "categories"=>["Bug Risk"], "remediation_points"=>50000, "location"=>{"path"=>"", "positions"=>{"begin"=>{"line"=>0, "column"=>0}, "end"=>{"line"=>0, "column"=>0}}}}`.
```
