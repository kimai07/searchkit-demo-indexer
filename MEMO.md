## node_modules/@searchkit/cli/lib/index.d.ts

```ts
export interface SearchkitField {
    facet?: boolean;
    stored?: boolean;
    fieldName: string;
    searchable?: boolean;
    type?: 'integer' | 'date' | 'float' | 'geo_point';
    sourceOptions?: {
        path: string;
        path2?: string;
        transform?: (str: string, str2: string) => string | number;
    };
}
```

## node_modules/@searchkit/cli/lib/lib.js

```ts
const getDocs = (config) => {
    if (config.source) {
        return config.source.map((doc) => config.fields
            .map((field) => {
            var _a;
            const value = field.sourceOptions ? doc[field.sourceOptions.path] : null;
            const value2 = field.sourceOptions ? doc[field.sourceOptions.path2] : null;
            return {
                [field.fieldName]: ((_a = field.sourceOptions) === null || _a === void 0 ? void 0 : _a.transform) ? field.sourceOptions.transform(value, value2)
                    : value
            };
        })
            .reduce((sum, value) => (Object.assign(Object.assign({}, sum), value)), {}));
    }
};
```

## bike-hire-stations/config.ts (parksの場合は変更不要)

```json
	sourceOptions: {
        path: 'latitude',
        path2: 'longitude',
        transform:(str, str2) => {
            return `${str},${str2}`
        }
	}
```