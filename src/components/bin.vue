// methods: {
    //     addCity() {
    //         if(localStorage.getItem('savedCities') === null) {
    //             this.savedCities = JSON.parse(localStorage.getItem('savedCities') || '{}');
    //         }
    //         const locationObj = {
    //           id: uid(),
    //           state: this.route.params.state,
    //           city: this.route.params.city,
    //           coords: {
    //             lat: this.route.params.lat,
    //             lng: this.route.params.lng,
    //           }
    //         }
    //         const cities = this.savedCities
    //         this.savedCities.push(locationObj);
    //         localStorage.setItem('savedCities', JSON.stringify(this.savedCities));
    //         let query = Object.assign({}, this.route.query);
    //         delete query.preview;
    //         this.router.replace({ query })
    //     },
    // },